---
layout: default
title: ODE Examples
nav_order: 1
parent: Examples
has_children: true
---

Given the ODE
\begin{array}{c}
x'(t) = f(t, x(t), u(t)), \ \ t \in [0,T], \
x(0) = x_0,
\end{array}
with $x(t)$ and $u(t)$ being the state and control variables respectively. The main goal is to find the control $u(t)$ that optimizes a certain functional $J(x(t),u(t))$.
Summarizing, control of ODEs is crucial when the main interest is not to find the solution $x(t)$ of the ODE, but instead to optimize a certain quantity $J(x(t),u(t))$ with respect to the control variable $u(t)$ and subject to the ODE.