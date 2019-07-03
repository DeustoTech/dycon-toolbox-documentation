---
layout: default
title: Home
nav_order: 1
---

# A MATLAB library which serves for the calculation of non-linear control problems.
---
<h4> Table of Contents</h4>
- [Symbolic Interface](#1)
- [Modular Structure](#2)
- [Direct and Indirect Methods](#3)
- [Tunnel to other platforms](#4)
  
---

 For each of these objects, we create different methods for the resolution of problems. </p> 

<p>The general formulation of these problems are: </p>

$$
\min_{u\in \Omega} J(y,u) \\
\dot{y} = F(t,y,u) \\ 
y(0) = y0
$$

<p>For each of these objects, we create different methods for problem resolution. In this way, we can easily choose the type of algorithm to solve the problem. For more information, continue exploring in our <a href="https://DeustoTech.github.io/dycon-toolbox-documentation/projects/01-documentation">documentation.</a></p>

<h2 id="1">Symbolic Interface</h2>

The symbolic interface of matlab makes the definition of problems easier. And in some cases, the problem can be solved analytically.

For example, DyCon Toolbox able to define a continuous state equations
```matlab
x = sym('x',[4 1]);
u = sym('u',[4 1]);
F = @(t,x,u) x + u;
```
With the **ode** class, we can create a structure with all information for solve an initial condition problem
```
idynamics = ode(F,x,u);
```
<h2 id="2">Modular Structure</h2>

DyCon Toolbox has been designed to easily accept different blocks of code. In this way, you can use another solver of the differential equations or other optimizers in any one programming language and taking advantage of all the interface already created. The first addition of de DyCon Toolbox is the acopling with the PDE Toolbox, native of MATLAB. In this way, we can use the mesh tool of the matlab to define and solve the PDE equation, and sovle de optimal control problem with DyCon Toolbox.

<h2 id="3">Direct and Indirect Methods</h2>
Main feature of DyCon Toolbox are the severals methods. The optimal control problems can be solve via full discretization or via resolve the optimal conditions.

- **Full Discretization (Direct Method)**
 
$$ 
    \vec{u}(t) \Rightarrow [ \vec{u}_1 ... \vec{u}_{N_t}] \\
    \vec{y}(t) \Rightarrow [ \vec{y}_1 ... \vec{y}_{N_t}] 
$$ 

- **Optimal Conditions (Indirect Methods)**

$$
    dJ = 0
$$

<h2 id="4"> Tunnel to other platforms</h2>
DyCon Toolbox is able to create a optimal control problem. The syntaxis of DyCon toolbox is very general and can be translate to other solver. For example, we have a translation of a AMPL/Ipopt.