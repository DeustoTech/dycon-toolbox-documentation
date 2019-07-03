---
layout: default
title: Control of Heat Equation
nav_order: 1
grand_parent: Examples
parent: PDE Examples
MATLAB: T0003_Laplacian

---
## Parametros de discretizacion

```matlab
N = 5;
xi = -1; xf = 1;
xline = linspace(xi,xf,N+2);
xline = xline(2:end-1);
dx = xline(2) - xline(1);
```

## Creamos el ODE

```matlab
A = FDLaplacian(xline);
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
a = -0.5; b = 0.5;
B = BInterior(xline,a,b,'min',false);
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
FinalTime = 0.2;
dt = 0.001;
Y0 =sin(0.5*pi*xline');

dynamics = pde('A',A,'B',B,'InitialCondition',Y0,'FinalTime',FinalTime,'Nt',5);
dynamics.mesh= xline;
```

## Creamos Problema de Control

```matlab
Y = dynamics.StateVector.Symbolic;
U = dynamics.Control.Symbolic;

YT = 0*cos(0.5*pi*xline');
epsilon = dx^4;
symPsi  = @(T,Y)   dx*(1/(2*epsilon))*(YT - Y).'*(YT - Y);
symL    = @(t,Y,U) dx*sum(abs(U));

iCP1 = Pontryagin(dynamics,symPsi,symL);
```

```matlab
iCP1.Target = YT;
```

## Solve Gradient

```matlab
tol = 1e-5;
%%
U0 = zeros(iCP1.Dynamics.Nt,iCP1.Dynamics.ControlDimension);
[UOptDyCon,JOptDycon] = GradientMethod(iCP1,U0,'tol',tol,'Graphs',false,'DescentAlgorithm',@ConjugateDescent,'MaxIter',300,'display','all')
%% %%%% fmincon
%% options = optimoptions(@fminunc,'display','iter','SpecifyObjectiveGradient',true);
%% UoptFminCon = fminunc(@(U) Control2Functional(iCP1,U),U0,options)
%%
%% %%%%
%% DynFminCon = copy(iCP1.Dynamics);
%% DynFminCon.label = 'Dycon Toolbox';
%% solve(DynFminCon,'Control',UoptFminCon)
%% %%%%
%% DynDyCon = copy(iCP1.Dynamics);
%% solve(DynDyCon,'Control',UOptDyCon)
%% DynDyCon.label = 'MATLAB - fmincon';
%% %%%%
%% solve(iCP1.Dynamics,'Control',U0)
%% iCP1.Dynamics.label = 'Free Dynamics';
```


```
Warning: The Optimal length step of Conjugate Gradient is zero. Possible local
minimum. 
    "error = 2.886088e-01 | Functional = 5.268280e-01 | norm(Gradient) = 1.889017e+00 | norm(U) = 6.545252e+00 | iter = 3"


    Solve with precision: 

        We obtain: J(u) = 5.268280E-01

        error = 2.886088E-01

    With 3 iterations,     In 0.070407 seconds


UOptDyCon =

         0    1.1435   -0.0000   -1.1435         0
         0    1.6522   -0.0000   -1.6522         0
         0    2.3820   -0.0000   -2.3820         0
         0    3.4218   -0.0000   -3.4218         0
         0         0         0         0         0


JOptDycon =

    0.5268


```

```matlab
%%animation([DynFminCon DynDyCon, iCP1.Dynamics],'YLim',[-0.1 0.1],'YLimControl',[-50 50],'xx',0.025,'Target',YT)
```

```matlab
U = iCP1.Dynamics.Control.Numeric;
Y = iCP1.Dynamics.StateVector.Numeric;

YU = 0*[Y U];
Udim = dynamics.ControlDimension;
Ydim = dynamics.StateDimension;
GetSymCrossDerivatives(iCP1);
GetSymCrossDerivatives(iCP1.Dynamics);

options = optimoptions('fmincon','display','iter', ...
                                 'MaxFunctionEvaluations',1e6, ...
                                 'SpecifyObjectiveGradient',true, ...
                                 'SpecifyConstraintGradient',true, ...
                                 'CheckGradients',true);

funobj = @(YU) StateControl2DiscrFunctional(iCP1,YU(:,1:Ydim),YU(:,Ydim+1:end));
fmincon(funobj,YU, ...
           [],[], ...
           [],[], ...
           [],[], ...
           @(UY) ConstraintDynamics(iCP1,YU(:,1:Ydim),YU(:,Ydim+1:end)),    ...
           options);

%% iCP1.ode
```


```
Unable to perform assignment because the size of the left side is 1-by-10 and the size of the right side is 5-by-1.

Error in AbstractOptimalControl/ConstraintDynamics (line 20)
    F(it,:) = Fnum(tspan(it),Y(it,:)',U(it,:)',Params);

Error in tp0d171630_859b_4452_a8c1_3fb0924c0ae7>@(UY)ConstraintDynamics(iCP1,YU(:,1:Ydim),YU(:,Ydim+1:end))

Error in fmincon (line 650)
      [ctmp,ceqtmp,initVals.gnc,initVals.gnceq] = feval(confcn{3},X,varargin{:});

Error in tp0d171630_859b_4452_a8c1_3fb0924c0ae7 (line 76)
fmincon(funobj,YU, ...

Caused by:
    Failure in initial nonlinear constraint function evaluation. FMINCON cannot continue
```

