---
layout: default
title: Computation of a control for a semilinear semi-discrete heat equation and analogies with a collective behavior model
nav_order: 1
grand_parent: Examples
parent: PDE Examples
---
## Semi-linear semi-discrete heat equation and collective behavior


In this tutorial we will apply the DyCon toolbox to find a control to the semi-discrete semi-linear heat equation.


$$y_t-N^2Ay=G(y)+Bu$$


where $N^2A$ is the discretization of the Laplacian in 1d in $N$ nodes. We are looking for a control that after time $T$ steers the system near zero. In order to do so we will frame the problem as a minimization of a functional and we will apply gradient descent to find it. Note that the convexity of the fuctional is not proven, therefore, we will obtain a local minima for the functional. The functional considered will be:


$$J(\boldsymbol{y},\boldsymbol{u})=|\boldsymbol{y}(t)|_{L^2}^2+\int_0^T `\boldsymbol{u}(t)`_{L^2}^2 dt$$


where by $|\cdot|_{L^2}$ we understand the discrete $L^2$ norm.


Once this control is computed for a certain N, we will think on a dynamical system that models an opinion dynamics with $N$ agents communicating through a chain.


\begin{equation}\label{m1}y_t-\frac{1}{N}Ay=G(y)+Bv\end{equation}


The goal will be to compute also the control $v$ thinking model \eqref{m1} as if it was a semidiscretization of a heat equation with diffusivity $\frac{1}{N^3}$. Furthermore we will also compute the control for model \eqref{m1} with the non-linearity being non-homogeneous on $N$ and a time horizon being $T_N=N^3T$.


Definition of the time

```matlab
syms t
%% Discretization of the space
N = 50;
xi = 0; xf = 1;
xline = linspace(xi,xf,N);
```


Interior Control region between 0.5 and 0.8

```matlab
w1=0.5;
w2=0.8;
```


Here we count how many elements in the discretization should be placed inside the control region

```matlab
count=1;
for i=1:N
    if (double(i-1))/double(N) > w1
        if (i-1)/double(N) < w2
            count=count+1;
        end
    end
end
```


we define symbolically the vectors of the state and the control

```matlab
symY = SymsVector('y',N);
symU = SymsVector('u',count);
```


We create the functional that we want to minimize Our goal is to set the system to zero penalizing the norm of the control by a parameter $\beta$ that will be small.

```matlab
YT = 0*xline.';

dx = xline(2) - xline(1);
beta = dx^4;
symPsi  = @(T,symY)(1/beta)*(YT - symY).'*(YT - symY);
symL    =@(t,symY,symU)(symU.'*symU)*(abs(w1-w2))/count;
```


We create the ODE object Our ODE object will have the semi-discretization of the semilinear heat equation. We set also initial conditions, define the non linearity and the interaction of the control to the dynamics.


Initial condition

```matlab
Y0 = 2*sin(pi*xline);
```


Diffusion part: the discretization of the 1d Laplacian

```matlab
A=(N^2)*(full(gallery('tridiag',N,1,-2,1)));
```


We define the matrix B that will be the effect of the interior control to the dynamics

```matlab
B = zeros(N,count);
count2=1;
for i=1:N
    if (i-1)/double(N) >= w1
        if (i-1)/double(N) < w2
            B(i,count2)=1;
            count2=count2+1;
        end
    end
end
```


Definition of the non-linearity $$ \partial_y[-5\exp(-y^2)] $$

```matlab
syms x;
syms G(x);
syms U(x);
syms DG(x);
U(x)=-5*exp(-x^2);
G(x)=diff(U,x);
formula=G(x);
G = symfun(formula,x)
```


```
 
G(x) =
 
10*x*exp(-x^2)
 

```


and we define the part of the dynamics corresponding to the nonlinearity

```matlab
vectorF = arrayfun( @(x)G(x),symY);
```


Putting all the things together

```matlab
Fsym  = A*symY + vectorF + B*symU;
F     = matlabFunction(Fsym,'Vars',{t,symY,symU,sym.empty});
```


Creation of the ODE object Time horizon

```matlab
T = 1;
```


We create the ODE-object and we change the resolution to $dt=0.01$ in order to see the variation in a small time scale. We will get the values of the solution in steps of size odeEqn.dt, if we do not care about modifying this parameter in the object, we might get the solution in certain time steps that will hide part of the dynamics.

```matlab
odeEqn = pde(F,symY,symU,'InitialCondition',Y0,'FinalTime',T);
odeEqn.Nt=100;
odeEqn.Solver = @ode23tb;
```


```
Error using ode/set.InitialCondition (line 353)
The Initial Condition must be a matrix: [50x1]

Error in ode (line 264)
             obj.InitialCondition = p.Results.InitialCondition;

Error in pde (line 1)
classdef pde < ode

Error in tp1f2196ec_d2de_4a75_aab8_e2284f0fd8dd (line 122)
odeEqn = pde(F,symY,symU,'InitialCondition',Y0,'FinalTime',T);

```


We solve the equation and we plot the free solution applying solve to odeEqn and we plot the free solution.

```matlab
solve(odeEqn)
```

```matlab
figure;
SIZ=size(odeEqn.StateVector.Numeric);
time=linspace(0,T,SIZ(1));
space=linspace(1,N,N);
[TIME,SPACE]=meshgrid(time,space);
surf(TIME',SPACE',odeEqn.StateVector.Numeric,'EdgeColor','none');
title('Free Dynamics')
ylabel('space discretization')
xlabel('Time')
```


We create the object that collects the formulation of an optimal control problem  by means of the object that describes the dynamics odeEqn, the functional to minimize Jfun and the time horizon T

```matlab
iCP1 = Pontryagin(odeEqn,symPsi,symL);
```


We apply the steepest descent method to obtain a local minimum (our functional might not be convex).

```matlab
U0 = zeros(length(iCP1.Dynamics.tspan),iCP1.Dynamics.ControlDimension);
%%GradientMethod(iCP1,U0,'display','all','DescentAlgorithm',@AdaptativeDescent)
options = optimoptions(@fminunc,'SpecifyObjectiveGradient',true,'display','iter');
fminunc(@(U) Control2Functional(iCP1,U),U0,options)
```

```matlab
figure;
SIZ=size(iCP1.Dynamics.StateVector.Numeric);
time=linspace(0,T,SIZ(1));
space=linspace(1,N,N);
[TIME,SPACE]=meshgrid(time,space);
surf(TIME',SPACE',iCP1.Dynamics.StateVector.Numeric,'EdgeColor','none')
title('Controlled Dynamics')
ylabel('space discretization')
xlabel('Time')
```


The control function inside the control region

```matlab
figure;
SIZ=size(iCP1.Dynamics.Control.Numeric);
time=linspace(0,T,SIZ(1));
space=linspace(1,SIZ(2)-1,SIZ(2)-1);
[TIME,SPACE]=meshgrid(time,space);
surf(TIME',SPACE',iCP1.Dynamics.Control.Numeric(:,1:SIZ(2)-1),'EdgeColor','none')
title('Control')
ylabel('space discretization')
xlabel('Time')
```

```matlab
figure;
line(xline,YT,'Color','red')
line(xline,odeEqn.StateVector.Numeric(end,:),'Color','blue')
line(xline,iCP1.Dynamics.StateVector.Numeric(end,:),'Color','green')
legend('Target','Free Dynamics','controlled dynamics')
```


Now we apply the same procedure for the collective behavior dynamics.


We will employ a function that does the algorithm explained before for the semilinear heat equation having the chance to set a diffusivity constant.


We set the parameters for the function

```matlab
beta=0.0000001;
y0=@(x)2*sin(pi*x);
syms x
syms G(x);
syms U(x);
syms DG(x);
U(x)=-5*exp(-x^2);
G(x)=diff(U,x);
T=1;
N=50;
```


For the simulation of the model in collective behavior we will employ a diffusivity $D=\frac{1}{N^3}$.

```matlab
[a,b,c,d]=SLSD1doptimalnullcontrol_T007_semilinear(N,1/(N^3),G,T,beta,[0.5,0.8],y0);
```

```matlab
figure;
surf(a.time,a.space,a.value,'EdgeColor','none');
title('Free Dynamics')
ylabel('space discretization')
xlabel('Time')
```

```matlab
figure;
surf(b.time,b.space,b.value,'EdgeColor','none')
title('Controlled Dynamics')
ylabel('space discretization')
xlabel('Time')
```

```matlab
figure;
surf(c.time,c.space,c.value,'EdgeColor','none')
title('Control')
ylabel('space discretization')
xlabel('Time')
```

```matlab
xline = linspace(xi,xf,N);
figure;
line(xline,d.y1,'Color','red')
line(xline,d.y2,'Color','blue')
line(xline,d.y3,'Color','green')
legend('Target','Free Dynamics','controlled dynamics')
```


Now we will change also the time horizon and we will incorporate a non-homogeneous non-linearity, we will just divide the non-linearity $G$ by $N^3$

```matlab
[a,b,c,d]=SLSD1doptimalnullcontrol_T007_semilinear(N,1/(N^2),G/(N^2),N^2*T,beta,[0.5,0.8],y0);
```

```matlab
figure;
surf(a.time,a.space,a.value,'EdgeColor','none');
shading interp; colormap jet
title('Free Dynamics')
ylabel('space discretization')
xlabel('Time')
```

```matlab
figure;
surf(b.time,b.space,b.value,'EdgeColor','none')
shading interp; colormap jet
title('Controlled Dynamics')
ylabel('space discretization')
xlabel('Time')
```

```matlab
figure;
surf(c.time,c.space,c.value,'EdgeColor','none')
shading interp; colormap jet
title('Control')
ylabel('space discretization')
xlabel('Time')
```

```matlab
figure;
xline = linspace(xi,xf,N);
line(xline,d.y1,'Color','red')
line(xline,d.y2,'Color','blue')
line(xline,d.y3,'Color','green')
legend('Target','Free Dynamics','controlled dynamics')
```

