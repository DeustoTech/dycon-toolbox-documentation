---
layout: default
title: Optimal control problem definition
nav_order: 4
has_children: true
---

### Example

We can create the optimal control problem

```matlab
% Get Symbolical variable
Ys  = iode.State.sym;
Us  = iode.Control.sym;
ts  = SX.sym('t'); %% <= Create a symbolical time
% Set Target
YT = zeros(2*M, 1);
%
PathCost  = casadi.Function('L'  ,{ts,Ys,Us},{ (1/2)*(Us'*Us)           });
FinalCost = casadi.Function('Psi',{Ys}      ,{  1e7*((Ys-YT).'*(Ys-YT)) });
% Create the optimal control
iocp = ocp(iode,PathCost,FinalCost);
```
