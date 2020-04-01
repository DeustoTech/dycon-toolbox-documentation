---
layout: default
title: Dynamics definition
nav_order: 3
has_children: true
---

<h3> Example of dynamic </h3>
In dynamics, the Van der Pol oscillator is a non-conservative oscillator with non-linear damping. It evolves in time according to the second-order differential equation:

$${\displaystyle {d^{2}x \over dt^{2}}-\mu (1-x^{2}){dx \over dt}+x=u}$$

In vectorial form :

$$ \frac{d}{dt} \begin{bmatrix} x \\ v                      \end{bmatrix} = 
                \begin{bmatrix} v \\ \mu(1-x^2)v  - x + u   \end{bmatrix}$$

```matlab
>> import casadi.*
>> x = SX.sym('x',[1 1]);
>> v = SX.sym('x',[1 1]);
>> u = SX.sym('u',[1 1]);
>> t = SX.sym('t');
>> mu = 10;
>> f = casadi.Function('f',{t,[x;v],u},{ [             v            ; ...
>>                                           mu*(1-x^2)*v - x + u   ] });
```
We can define the  `ode` command to build a MATLAB object 
```matlab
>> T  = 5;
>> Nt = 100;
>> tspan = linspace(0,T,Nt);
>> % Build a ode object
>> idyn = ode(f,[x;v],u,tspan);
>> idyn.InitialCondition = [2,4]';
```
Inside this object, we have a lot information of dynamics


Solve dynamics with zeros control
```matlab
>> u0 = ZerosControl(idyn);
>> wt = solve(idyn,u0)
```
