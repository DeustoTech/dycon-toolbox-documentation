---
layout: default
title: Rotor Control
nav_order: 1
grand_parent: Examples
parent: ODE Examples
MATLAB: T06ODET0002_spin

---
```matlab
clear;
```

```matlab
syms t
symY = SymsVector('y',4);
symU = SymsVector('u',4);
```

## Dynamics

```matlab
T = 20;
Y0 = [2,3.2,1,4].';
Fsym  = @(t,Y,U,Params) U;

dynamics = ode(Fsym,symY,symU,'InitialCondition',Y0,'FinalTime',T);
dynamics.Solver =  @eulere;
dynamics.Nt = 150;
%%dynamics.SolverParameters = {odeset('RelTol',1e-1,'AbsTol',1e-1)};


%%
beta=1;
alphaone=0.0392; %%in the pdf "draft_Marposs3.pdf", this parameter is "\alpha_1".
alphatwo=24.5172; %%in the pdf "draft_Marposs3.pdf", this parameter is "\alpha_2".

symPsi  = @(T,Y) 0;
symL    = @(t,Y,U) (U(1)^2+U(2)^2+U(3)^2+U(4)^2)+ ...
          (0.5)*(beta*alphaone)*((-(sin(Y(1))+sin(Y(2))+sin(Y(3))+sin(Y(4))))^2  + ...
                                   (cos(Y(1))+cos(Y(2))+cos(Y(3))+cos(Y(4)) )^2) + ...
          (0.5)*(beta*alphatwo)*(  (sin(Y(4))+sin(Y(3))-sin(Y(2))-sin(Y(1)) )^2   + ...
                                   (cos(Y(1))+cos(Y(2))-cos(Y(3))-cos(Y(4)) )^2);
```


For last, you an create the functional object


Creta the control Problem

```matlab
iCP1 = Pontryagin(dynamics,symPsi,symL);
```

```matlab
%% AMPL Neos Server
AMPLFileFixedFinalTime(iCP1,'AMPL.txt')
outfile = SendNeosServer('AMPL.txt');
```


```
Output in: /home/djoroya/Documentos/GitHub/DyCon-toolbox/tmp/AMPL-executions/02-Jul-2019-13-25-147948-097541-AMPL.txt/AMPL.txt.out


```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/ODE/T06ODET0002/copiaRM_01.png)


## Read Data

```matlab
AMPLSolution  = NeosLoadData(outfile);
```

## Solve Gradient

```matlab
U = zeros(dynamics.Nt,dynamics.ControlDimension);
Y = zeros(dynamics.Nt,dynamics.StateDimension);

GetSymCrossDerivatives(iCP1)

GetSymCrossDerivatives(iCP1.Dynamics)

YU0 = [Y U];
Udim = dynamics.ControlDimension;
Ydim = dynamics.StateDimension;

options = optimoptions('fmincon','display','iter',    ...
                       'MaxFunctionEvaluations',1e6,  ...
                       'SpecifyObjectiveGradient',true, ...
                       'CheckGradients',false,          ...
                       'SpecifyConstraintGradient',true, ...
                       'HessianFcn',@(YU,Lambda) Hessian(iCP1,YU,Lambda));
%%
funobj = @(YU) StateControl2DiscrFunctional(iCP1,YU(:,1:Ydim),YU(:,Ydim+1:end));

clear ConstraintDynamics
YU = fmincon(funobj,YU0, ...
           [],[], ...
           [],[], ...
           [],[], ...
           @(YU) ConstraintDynamics(iCP1,YU(:,1:Ydim),YU(:,Ydim+1:end)),    ...
           options);

iCP1.Dynamics.StateVector.Numeric = YU(:,1:Ydim);
iCP1.Dynamics.Control.Numeric = YU(:,Ydim+1:end);
```


```
                                            First-order      Norm of
 Iter F-count            f(x)  Feasibility   optimality         step
    0       1    6.230187e+00    4.000e+00    0.000e+00
    1       4    9.237042e+00    1.224e+00    3.293e-01    8.660e+00
    2       6    1.165134e+01    7.973e-01    1.355e-01    4.330e+00
    3       7    1.977411e+01    5.829e-16    2.831e-01    8.660e+00
    4       9    1.889025e+01    5.343e-16    5.609e-01    8.660e+00
    5      10    1.541835e+01    5.759e-16    1.910e-01    8.660e+00
    6      13    1.440534e+01    8.661e-16    3.941e-01    1.516e+01
    7      15    1.215624e+01    7.078e-16    3.012e-01    1.516e+01
    8      17    1.016819e+01    8.383e-16    4.225e-01    1.516e+01
    9      18    7.483708e+00    7.421e-02    1.138e-01    3.606e+01
   10      19    7.375461e+00    1.140e-09    2.430e-02    2.456e+00
   11      20    7.371419e+00    5.615e-10    7.266e-04    3.191e-01
   12      21    7.371373e+00    3.057e-11    4.055e-06    1.109e-01

Local minimum found that satisfies the constraints.

Optimization completed because the objective function is non-decreasing in 
feasible directions, to within the default value of the optimality tolerance,
and constraints are satisfied to within the default value of the constraint tolerance.


```

```matlab
figure
subplot(2,2,1)
plot(iCP1.Dynamics.Control.Numeric(1:end-1,:),'.-')
title('DyCon Toolbox Control');
subplot(2,2,3)
plot(iCP1.Dynamics.StateVector.Numeric(1:end-1,:),'.-')
title('DyCon Toolbox State');
%%
subplot(2,2,2)
plot(AMPLSolution.Control','.-')
title('AMPL Control');
subplot(2,2,4)
plot(AMPLSolution.State','.-')
title('AMPL State');

figure
subplot(1,2,1)
plot(iCP1.Dynamics.Control.Numeric(1:end-1,:) - AMPLSolution.Control(:,1:end-1)','.-')
title('Diff Control');

subplot(1,2,2)
plot(iCP1.Dynamics.StateVector.Numeric(1:end-1,:) - AMPLSolution.State(:,1:end-1)','.-')
title('Diff State');
```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/ODE/T06ODET0002/copiaRM_02.png)

![]({{site.url}}/{{site.baseurl}}/assets/imgs/ODE/T06ODET0002/copiaRM_03.png)

