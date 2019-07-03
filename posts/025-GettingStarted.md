---
layout: default
title: Getting Started
nav_order: 2.5
---
Dycon Toolbox is an environment under the paradigm of object-oriented programming. We create objects to define control problems. We can see an example of this in a general optimal control problem: 

$$ \min_{U \in \Omega} [ \Psi (Y(T),t) + \int_0^T L(Y,U,t)dt] $$

subject to:

$$ \dot{Y} = f(t,Y,U) \text{  where } Y(0) = Y_0$$


In object-oriented programming, this problem can be described through the following scheme:


In this way, we can create algorithms to solve different problems following the same underneath structure, and the solutions of those problems are independent on the solver employed. 

