---
layout: default
title: PDE Examples
nav_order: 2
parent: Examples
has_children: true

---

Control of PDEs can be approached by the DyCon Toolbox for all evolutionary PDEs that can be written in a semidiscrete form leading                       to the following finite dimensional system 

$$
\begin{array}{c}
\frac{\partial x(t)}{\partial t} =
L(t, x(t), u(t)), \ \ t \in [0,T], \
x(0) = x_0,
\end{array} $$

with $x(t)$ and $u(t)$ being the state and control variables respectively. The target is to find the control $u(t)$ that optimizes the functional $J(x(t),u(t))$ subject to the semidiscrete PDE.