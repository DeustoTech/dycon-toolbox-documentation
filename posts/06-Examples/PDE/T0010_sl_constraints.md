---
layout: default
title: Population Dynamics
nav_order: 1
grand_parent: Examples
parent: PDE Examples
---
## Semi-linear semi-discrete heat equation and collective behavior


Definition of the time

```matlab
clear
syms t
%% Discretization of the space
N = 10;
L = 1;
xi = 0; xf = L;
xline = linspace(xi,xf,N+2);
xline = xline(2:end-1);
```

```matlab
symY = SymsVector('y',N);
symU = SymsVector('u',1);
```


We create the functional that we want to minimize Our goal is to set the system to zero penalizing the norm of the control by a parameter $\beta$ that will be small.

```matlab
YT = 0.2 + 0*xline';
dx = xline(2) - xline(1);
symPsi  = @(T,symY) (YT - symY).'*(YT - symY);
%%tiempo= @(t) piecewise(t<=T/2,500,t>T/2,0);
symL    = @(t,symY,symU) 0 ;
```


We create the ODE object Our ODE object will have the semi-discretization of the semilinear heat equation. We set also initial conditions, define the non linearity and the interaction of the control to the dynamics.


Initial condition

```matlab
%%Y0 = 2*sin(pi*xline)';
Y0 = 0.99+0*xline';
```


Diffusion part: the discretization of the 1d Laplacian

```matlab
A=(N^2/L^2)*(full(gallery('tridiag',N,1,-2,1)));
%% A(1,1)=0;
%% A(1,2)=0;
%% A(end,end)=0;
%% A(end,end-1)=0;
```


We define the matrix B that will be the effect of the interior control to the dynamics

```matlab
B = zeros(N,1);
B(1,1) = 1;
B(end,end) = 1;
B = (N^2/L^2)*B;
```


Definition of the non-linearity $$ \partial_y[-5\exp(-y^2)] $$

```matlab
syms x;
syms G(x);
syms U(x);
syms DG(x);
%%U(x)=-5*exp(-x^2);
%%G(x)=diff(U,x);
G(x)=x*(1-x)*(x-0.2);
formula=G(x);
G = symfun(formula,x)
```


```
 
G(x) =
 
-x*(x - 1)*(x - 1/5)
 

```


and we define the part of the dynamics corresponding to the nonlinearity

```matlab
vectorF = arrayfun( @(x)G(x),symY);
```

```matlab
%% Putting all the things together
Fsym  = A*symY + vectorF + B*symU;
syms t
Fsym_fh = matlabFunction(Fsym,'Vars',{t,symY,symU,sym.empty});
```

```matlab
odeEqn = pde(Fsym_fh,symY,symU,'InitialCondition',Y0,'FinalTime',2.0);
odeEqn.Nt=20;
odeEqn.mesh = xline;
odeEqn.Solver = @ode23tb;
```


We solve the equation and we plot the free solution applying solve to odeEqn and we plot the free solution.

```matlab
solve(odeEqn)
```


```

ans =

  Columns 1 through 7

         0    0.1053    0.2105    0.3158    0.4211    0.5263    0.6316

  Columns 8 through 14

    0.7368    0.8421    0.9474    1.0526    1.1579    1.2632    1.3684

  Columns 15 through 20

    1.4737    1.5789    1.6842    1.7895    1.8947    2.0000


```

```matlab
figure;
surf(odeEqn.StateVector.Numeric,'EdgeColor','none');
title('Free Dynamics')
ylabel('space discretization')
xlabel('Time')
```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/PDE/T0010/copiaRM_01.png)

We create the object that collects the formulation of an optimal control problem  by means of the object that describes the dynamics odeEqn, the functional to minimize Jfun and the time horizon T

```matlab
iCP1 = Pontryagin(odeEqn,symPsi,symL);
%%
iCP1.Constraints.MaxControl = 1;
iCP1.Constraints.MinControl = 0;
```

```matlab
AMPLFileFixedFinalTime(iCP1,'Domenec.txt')
out = SendNeosServer('Domenec.txt')

data = NeosLoadData(out)
```


```
Output in: /home/djoroya/Documentos/GitHub/DyCon-toolbox/tmp/AMPL-executions/02-Jul-2019-10-49-24649-913376-Domenec.txt/Domenec.txt.out


out =

    '/home/djoroya/Documentos/GitHub/DyCon-toolbox/tmp/AMPL-executions/02-Jul-2019-10-49-24649-913376-Domenec.txt/Domenec.txt.out'


data = 

  struct with fields:

       cost: 0
          T: 2
       Ydim: 10
       Udim: 1
      State: [10x20 double]
    Control: [1x20 double]


```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/PDE/T0010/copiaRM_02.png)

![]({{site.url}}/{{site.baseurl}}/assets/imgs/PDE/T0010/copiaRM_03.png)


```matlab
U = zeros(odeEqn.Nt,odeEqn.ControlDimension);
Y = zeros(odeEqn.Nt,odeEqn.StateDimension);

GetSymCrossDerivatives(iCP1)

GetSymCrossDerivatives(iCP1.Dynamics)

YU0 = [Y U];
Udim = odeEqn.ControlDimension;
Ydim = odeEqn.StateDimension;

options = optimoptions('fmincon','display','iter',    ...
                       'MaxFunctionEvaluations',1e6,  ...
                       'SpecifyObjectiveGradient',true, ...
                       'CheckGradients',false,          ...
                       'SpecifyConstraintGradient',true)%% , ...
                        %%'HessianFcn',@(YU,Lambda) Hessian(iCP1,YU,Lambda));
%%
funobj = @(YU) StateControl2DiscrFunctional(iCP1,YU(:,1:Ydim),YU(:,Ydim+1:end));

Yup = Y + Inf;
Ydown = Y - Inf;
Uup = Y + 1;
Udown = Y - 0;

YUdown = [Ydown Udown];
YUup = [Yup Uup];


clear ConstraintDynamics
YU = fmincon(funobj,YU0, ...
           [],[], ...
           [],[], ...
           YUdown,YUup, ...
           @(YU) ConstraintDynamics(iCP1,YU(:,1:Ydim),YU(:,Ydim+1:end)),    ...
           options);

iCP1.Dynamics.StateVector.Numeric = YU(:,1:Ydim);
iCP1.Dynamics.Control.Numeric = YU(:,Ydim+1:end);
```


```

options = 

  fmincon options:

   Options used by current Algorithm ('interior-point'):
   (Other available algorithms: 'active-set', 'sqp', 'sqp-legacy', 'trust-region-reflective')

   Set properties:
               CheckGradients: 0
                      Display: 'iter'
       MaxFunctionEvaluations: 1000000
    SpecifyConstraintGradient: 1
     SpecifyObjectiveGradient: 1

   Default properties:
                    Algorithm: 'interior-point'
          ConstraintTolerance: 1.0000e-06
     FiniteDifferenceStepSize: 'sqrt(eps)'
         FiniteDifferenceType: 'forward'
         HessianApproximation: 'bfgs'
                   HessianFcn: []
           HessianMultiplyFcn: []
                  HonorBounds: 1
                MaxIterations: 1000
               ObjectiveLimit: -1.0000e+20
          OptimalityTolerance: 1.0000e-06
                    OutputFcn: []
                      PlotFcn: []
                 ScaleProblem: 0
                StepTolerance: 1.0000e-10
          SubproblemAlgorithm: 'factorization'
                     TypicalX: 'ones(numberOfVariables,1)'
                  UseParallel: 0

   Options not used by current Algorithm ('interior-point')
   Default properties:
    FunctionTolerance: 1.0000e-06


Warning: Length of lower bounds is > length(x); ignoring extra bounds. 
Warning: Length of upper bounds is > length(x); ignoring extra bounds. 
Your initial point x0 is not between bounds lb and ub; FMINCON
shifted x0 to strictly satisfy the bounds.

                                            First-order      Norm of
 Iter F-count            f(x)  Feasibility   optimality         step
    0       1    4.000000e-01    4.500e+00    5.604e-01
    1       2    3.441430e-03    2.464e+00    5.604e-01    3.085e+00
    2       3    1.353704e-01    2.125e+00    4.102e-01    2.217e+00
    3       4    3.487871e-02    7.938e-01    1.838e-01    6.813e-01
    4       5    4.250682e-02    1.013e+00    1.838e-01    8.933e-01
    5       7    6.295185e-02    1.631e-01    1.000e-01    1.696e+00
    6       9    3.343353e-02    1.097e-01    5.271e-02    1.539e-01
    7      13    3.173097e-02    8.250e-02    3.630e-02    3.221e-02
    8      20    2.196572e-02    1.249e-02    1.985e-02    1.037e-01
    9      31    1.627775e-02    9.232e-03    1.542e-02    5.575e-02
   10      42    1.398909e-02    4.801e-03    1.331e-02    2.905e-02
   11      53    1.295050e-02    2.481e-03    1.228e-02    1.528e-02
   12      64    1.244847e-02    1.298e-03    1.176e-02    8.005e-03
   13      75    1.219707e-02    6.786e-04    1.150e-02    4.185e-03
   14      86    1.206873e-02    3.542e-04    1.136e-02    2.186e-03
   15      97    1.200255e-02    1.848e-04    1.129e-02    1.141e-03
   16     108    1.196824e-02    9.643e-05    1.125e-02    5.951e-04
   17     119    1.195039e-02    5.030e-05    1.123e-02    3.104e-04
   18     130    1.194110e-02    2.624e-05    1.122e-02    1.619e-04
   19     141    1.193626e-02    1.368e-05    1.122e-02    8.446e-05
   20     152    1.193374e-02    7.137e-06    1.122e-02    4.405e-05
   21     163    1.193242e-02    3.723e-06    1.122e-02    2.298e-05
   22     174    1.193173e-02    1.942e-06    1.121e-02    1.198e-05
   23     185    1.193137e-02    1.013e-06    1.121e-02    6.251e-06
   24     196    1.193119e-02    5.282e-07    1.121e-02    3.260e-06
   25     207    1.193109e-02    2.755e-07    1.121e-02    1.700e-06
   26     218    1.193104e-02    1.437e-07    1.121e-02    8.869e-07
   27     229    1.193101e-02    7.494e-08    1.121e-02    4.626e-07
   28     240    1.193100e-02    3.909e-08    1.121e-02    2.413e-07
   29     251    1.193099e-02    2.039e-08    1.121e-02    1.258e-07
   30     262    1.193099e-02    1.063e-08    1.121e-02    6.564e-08

                                            First-order      Norm of
 Iter F-count            f(x)  Feasibility   optimality         step
   31     273    1.193099e-02    5.546e-09    1.121e-02    3.423e-08
   32     284    1.193099e-02    2.893e-09    1.121e-02    1.786e-08
   33     295    1.193098e-02    1.509e-09    1.121e-02    9.313e-09
   34     306    1.193098e-02    7.869e-10    1.121e-02    4.857e-09
   35     317    1.193098e-02    4.104e-10    1.121e-02    2.533e-09
   36     328    1.193098e-02    2.141e-10    1.121e-02    1.321e-09
   37     339    1.193098e-02    1.117e-10    1.121e-02    6.892e-10

Local minimum possible. Constraints satisfied.

fmincon stopped because the size of the current step is less than
the default value of the step size tolerance and constraints are 
satisfied to within the default value of the constraint tolerance.


```


We apply the steepest descent method to obtain a local minimum (our functional might not be convex).

```matlab
iCP1.Constraints.MaxControl = [];
iCP1.Constraints.MinControl = [];
U0 = 0.0*(iCP1.Dynamics.tspan).' + 0.1;
U0(U0>1) = 1;
U0(U0<0) = 0;

%%U0 = zeros(length(iCP1.Dynamics.tspan),iCP1.Dynamics.ControlDimension)+ 0.6;
GradientMethod(iCP1,U0,'display','all','DescentAlgorithm',@AdaptativeDescent,'Graphs',false,'display','all')
```


```
    "error = 2.495887e+02 | Functional = 1.165603e-02 | norm(Gradient) = 8.833744e+01 | norm(U) = 5.079567e-01 | iter = 5"

    "error = 3.271382e+02 | Functional = 4.522516e-03 | norm(Gradient) = 1.725769e+02 | norm(U) = 5.627170e-01 | iter = 10"

    "error = 8.343149e+01 | Functional = 7.097202e-04 | norm(Gradient) = 3.564225e+01 | norm(U) = 5.418573e-01 | iter = 15"

    "error = 5.641796e+01 | Functional = 1.345175e-04 | norm(Gradient) = 2.951192e+01 | norm(U) = 5.535245e-01 | iter = 20"

    "error = 2.471906e+01 | Functional = 4.610182e-05 | norm(Gradient) = 1.122387e+01 | norm(U) = 5.499869e-01 | iter = 25"

    "error = 7.195390e+00 | Functional = 3.412853e-06 | norm(Gradient) = 3.892319e+00 | norm(U) = 5.524512e-01 | iter = 30"

    "error = 2.449993e+00 | Functional = 1.080842e-06 | norm(Gradient) = 1.025122e+00 | norm(U) = 5.521550e-01 | iter = 35"

    "error = 1.311006e+00 | Functional = 6.093864e-07 | norm(Gradient) = 7.168544e-01 | norm(U) = 5.524957e-01 | iter = 40"

    "error = 1.956110e+00 | Functional = 4.113095e-07 | norm(Gradient) = 9.446526e-01 | norm(U) = 5.523669e-01 | iter = 45"

    "error = 3.776324e-01 | Functional = 3.491644e-07 | norm(Gradient) = 1.900762e-01 | norm(U) = 5.524779e-01 | iter = 50"

Warning:  Length Step =8.7399e-11
 The Min Length Step of the Adaptative Descent has been achieve 
    "error = 3.776324e-01 | Functional = 3.491644e-07 | norm(Gradient) = 1.900762e-01 | norm(U) = 5.524779e-01 | iter = 51"


    Solve with precision: 

        We obtain: J(u) = 3.491644E-07

        error = 3.776324E-01

    With 51 iterations,     In 23.1484 seconds


```


U0 = zeros(length(iCP1.Dynamics.tspan),iCP1.Dynamics.Udim)+ 0; options = optimoptions(@fminunc,'SpecifyObjectiveGradient',true,'display','iter'); fminunc(@(U) Control2Functional(iCP1,U),U0,options)

```
options = optimoptions('ga','display','iter', ...
                             'HybridFcn',{'fmincon','SpecifyObjectiveGradient',true},'UseParallel',false);
ga(@(U) Control2Functional(iCP1,U'),odeEqn.Nt,[],[],[],[],U0*0 ,U0*0 + 1,[],options)
```

```matlab
options = optimoptions(@fmincon,'SpecifyObjectiveGradient',true,'display','iter');
U0 = zeros(length(iCP1.Dynamics.tspan),iCP1.Dynamics.ControlDimension)+ 0.66;
U0 = 0.1*(iCP1.Dynamics.tspan.^0.5).';

fmincon(@(U) Control2Functional(iCP1,U),U0,[],[], ...
                                           [],[], ...
                                           U0*0 ,U0*0 + 1, ... %% lb - yp
                                           [],options)
```


```
Your initial point x0 is not between bounds lb and ub; FMINCON
shifted x0 to strictly satisfy the bounds.

                                            First-order      Norm of
 Iter F-count            f(x)  Feasibility   optimality         step
    0       1    4.011409e-02    0.000e+00    2.596e+01
    1       3    2.965813e-01    0.000e+00    1.236e+02    4.730e-01
    2       4    5.088681e-01    0.000e+00    2.743e+01    1.373e+00
    3       6    3.454403e-02    0.000e+00    1.336e+01    4.188e-01
    4       8    3.052231e-03    0.000e+00    1.159e+01    1.874e-01
    5      10    5.239095e-04    0.000e+00    5.981e+00    1.029e-01
    6      11    7.108739e-05    0.000e+00    6.325e-01    1.232e-01
    7      12    4.890576e-04    0.000e+00    7.550e-01    4.691e-02
    8      13    1.012729e-03    0.000e+00    1.076e-01    4.817e-02
    9      29    1.010862e-03    0.000e+00    9.708e-02    2.264e-06

Local minimum possible. Constraints satisfied.

fmincon stopped because the size of the current step is less than
the default value of the step size tolerance and constraints are 
satisfied to within the default value of the constraint tolerance.


ans =

    0.4990
    0.5013
    0.5007
    0.5002
    0.4998
    0.4995
    0.4992
    0.4989
    0.4985
    0.4981
    0.4975
    0.4964
    0.4940
    0.4879
    0.4622
    0.4299
    0.3623
    0.2509
    0.1414
    0.1960


```

```matlab
figure;
SIZ=size(iCP1.Dynamics.StateVector.Numeric);

surf(iCP1.Dynamics.StateVector.Numeric,'EdgeColor','none')
title('Controlled Dynamics')
ylabel('space discretization')
xlabel('Time')
```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/PDE/T0010/copiaRM_04.png)

The control function inside the control region

```matlab
figure;
%% SIZ=size(iCP1.Dynamics.Control.Numeric);
%% time=linspace(0,T,SIZ(1));
%% space=linspace(1,SIZ(2)-1,SIZ(2)-1);
%% [TIME,SPACE]=meshgrid(time,space);
%% surf(iCP1.Dynamics.Control.Numeric,'EdgeColor','none')
%% title('Control')
%% ylabel('space discretization')
%% xlabel('Time')
plot(iCP1.Dynamics.Control.Numeric)
```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/PDE/T0010/copiaRM_05.png)


```matlab
figure;
line(xline,YT,'Color','red')
line(xline,odeEqn.StateVector.Numeric(end,:),'Color','blue')
line(xline,iCP1.Dynamics.StateVector.Numeric(end,:),'Color','green')
legend('Target','Free Dynamics','controlled dynamics')
```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/PDE/T0010/copiaRM_06.png)


```matlab
error('sda')
```


```
Error using ./imgs-matlab/copiaRM (line 198)
sda

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


