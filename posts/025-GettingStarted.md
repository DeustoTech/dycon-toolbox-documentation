---
layout: default
title: Getting Started
nav_order: 2.5
---
Dycon Toolbox is an environment under the paradigm of object-oriented programming. We create objects to define control problems. We can see an example of this in a general optimal control problem: 

$$ \min_{U \in \Omega} [ \Psi (Y(T),t) + \int_0^T L(Y,U,t)dt] $$

subject to:

$$ \dot{Y} = f(t,Y,U) \text{  where } Y(0) = Y_0$$


DyCon Toolbox tries to solve this problem from different known methods. To be able to easily compare them and choose the most appropriate method for each type of problem. In this way control problems are objects and resolution algorithms are methods associated with these objects.

The idea is that the different algorithms produce the same solution structure so that other methods of visualization and comparison can be used independent of the resolution algorithm.


