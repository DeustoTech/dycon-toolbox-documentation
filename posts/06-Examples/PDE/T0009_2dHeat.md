---
layout: default
title: Heat Equation 2D
nav_order: 1
grand_parent: Examples
parent: PDE Examples
---
```matlab
clear;

Nx = 10;    Ny = 15;
%%
xline = linspace(-1,1,Nx+2); xline = xline(2:end-1); dx = xline(2) - xline(1);
yline = linspace(-1,1,Ny+2); yline = yline(2:end-1); dy = yline(2) - yline(1);
%%
[~,~,A] = laplacian([Nx,Ny],{'NN' 'NN'});

A = (1/(dx*dy)^2)*A;
```


```
  
Elapsed time is 0.004981 seconds.
The Laplacian matrix takes 14808 bytes
  

```

## Dynamics

```matlab
dynamics = pde('A',A);
dynamics.mesh = {xline,yline};
dynamics.FinalTime = 2;
%% time points
Nt = 30;
dynamics.Nt =Nt;
```

## Select Initial Condition

```matlab
[Xms,Yms] = meshgrid(xline,yline);
Initms = Xms.^2 + Yms.^2;

dynamics.InitialCondition    =  reshape(Initms,Nx*Ny,1);
```

## Compute Target

```matlab
solve(dynamics)
FinalState =  dynamics.StateVector.Numeric(end,:);
```


```

ans =

  Columns 1 through 7

         0    0.0690    0.1379    0.2069    0.2759    0.3448    0.4138

  Columns 8 through 14

    0.4828    0.5517    0.6207    0.6897    0.7586    0.8276    0.8966

  Columns 15 through 21

    0.9655    1.0345    1.1034    1.1724    1.2414    1.3103    1.3793

  Columns 22 through 28

    1.4483    1.5172    1.5862    1.6552    1.7241    1.7931    1.8621

  Columns 29 through 30

    1.9310    2.0000


```

## Build Inverse Problem - dynamics and FinalState mamdatory

```matlab
InvP = InverseProblem(dynamics,FinalState);

dx = xline(2) - xline(1);
InvP.gamma = dx^4;
```

## Can add constraints in Init Condition

```matlab
InvP.Constraints.MinControl = 0;
InitControl = FinalState*0;

%%GradientMethod(InvP,InitControl)
GradientMethod(InvP,InitControl,'display','all','tol',1e-9,'DescentAlgorithm',@ConjugateDescent,'DescentParameters',{'StopCriteria','JDiff'})

%%InitControl = FinalState*0;
%%GradientMethod(InvP,InitControl,'display','all','tol',1e-9,'DescentAlg
```


```
Reference to non-existent field 'lineal'.

Error in AbstractOptimalControl/GradientMethod (line 134)
    if iCP.Dynamics.lineal == iCP.Adjoint.Dynamics.lineal

Error in tpbec78ca7_9173_4798_8441_1927d3dd77e9 (line 42)
GradientMethod(InvP,InitControl,'display','all','tol',1e-9,'DescentAlgorithm',@ConjugateDescent,'DescentParameters',{'StopCriteria','JDiff'})

```

