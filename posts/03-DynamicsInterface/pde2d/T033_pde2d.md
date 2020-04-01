---
layout: default
title: pde2d 
parent: Dynamics definition
nav_order: 1
has_children: true
---

MATLAB class to represents a dynamical systems.


<h2 id="1"> Constructor </h2>

#### Inputs 

<table>
    <tr>
        <th> Name </th>
        <th> Class</th>
        <th> Description </th>
    </tr>
    <tr>
        <td> dyn</td>
        <td>
            <font color="red">'casadi.Function'</font>
        </td>
        <td>
            It is a casadi object that define the dynamics equation $\mathbb{R}^+\times\mathcal{X}\times \mathcal{U} \rightarrow S$ of ODE.
        </td>
    </tr>
    <tr>
        <td> State</td>
        <td>
            <font color="red">'casadi.SX'</font>
        </td>
        <td>
            It is a symbolical variable that represent the state $x \in \mathcal{X}$
        </td>  
    </tr>
    <tr>
        <td> Control</td>
        <td>
            <font color="red">'casadi.SX'</font>
        </td>
        <td>
            It is a symbolical variable that represent the control $u \in \mathcal{U}$
        </td>  
    </tr>
    <tr>
        <td> tspan</td>
        <td>
            <font color="red">'double'</font>
        </td>
        <td>
            It is a list of times in which the dynamics will be solved.       
        </td>  
    </tr>
</table>

#### Outputs

<table>
    <tr>
        <th> Name </th>
        <th> Class</th>
        <th> Description </th>
    </tr>
    <tr>
        <td> iode</td>
        <td>
            <font color="red">'ode'</font>
        </td>
        <td>
           It is a DyCon Toolbox object to represent a ODE.
        </td>
    </tr>
</table>


```matlab
import casadi.*
% define the symbolical variables
Xs = SX.sym('x',2,1);
Us = SX.sym('u',2,1);
ts = SX.sym('ts');
% define the dynamics
dyn = casadi.Function('f',{ts,Xs,Us},{ -cos(1*pi*Xs) + 2*sin(ts)+ Us });
% choose the time discretization
T = 5;
tspan = linspace(0,T,50);
% create the ode object
isys = ode(dyn,Xs,Us,tspan);
```




