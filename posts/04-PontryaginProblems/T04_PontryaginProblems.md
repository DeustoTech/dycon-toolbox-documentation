---
layout: default
title: Pontryagin Problems 
nav_order: 4
has_children: true
---


The aim of this section is to give basis to solve analytically or numerically optimal
control problems.

In full generality, we consider a system governed by the dynamic:

$$ \dY = f(t,\Y(t),\U(t))$$

with $\Y \in R^n$  is the state variable and $\U \in R^m$

The control problems is:

Given $T > 0$, $\Y(0) = \Y_0$ and $\Y(T) = \Y_T$  does it exists  $\U : [0,T] \rightarrow R^m$ such that systems steers $\Y_0$ to $\Y_T$ in time $T$.


For optimal control problem, we consider a cost function:

$$ J(\Y, \U) =  \int^T_0 L(\Y(t), \U(t)) dt + \Psi(\Y(T), \U(T)) $$
