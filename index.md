---
layout: default
title: Home
nav_order: 1
---

# A MATLAB library for non-linear optimal control problems

DyCon toolbox is a library for MATLAB for optimal non-linear control. This uses the automatic differentiation of <a href="https://web.casadi.org/">CasADi</a> to compute all the derivatives necessary for its resolution. 

In this library you can use the two different approaches:

- **Direct method**: This are to discretize state and control, and reduce the problem to a nonlinear optimization problem (nonlinear programming). In this case, DyCon Toolbox is able to solve the problem through optimization in <a href="https://en.wikipedia.org/wiki/IPOPT">IPOPT</a>.
- **Indirect method**: This consists of solving the adjoint problem numerically backwards in time, and with this calculating the functional derivative of the problem. Then we can simply use methods based on gradient descent to obtain the optimal control.

Although direct methods are more common in the control community, when the problem has a very large state dimension, indirect methods are more efficient. That is why at DyCon Toolbox we unify the definition of control problems so that they can be solved from the most convenient approach.

### Features

- **Sparse symbolic variables and automatic differentiation via <a href="https://web.casadi.org/">CasADi</a>**
- **Direct method using <a href="https://coin-or.github.io/Ipopt/">Ipopt</a> Solver**
- **Indirect methods implemented (<a href="https://en.wikipedia.org/wiki/Pontryagin%27s_maximum_principle">Pontryagin's maximum principle</a>)**
- **Compatible with <a href="https://es.mathworks.com/products/pde.html">MATLAB PDE Toolbox</a>**
- **Easy to implement a new optimal control problems**
- **Many numerical schemes already implemented (<a href="https://en.wikipedia.org/wiki/List_of_Runge%E2%80%93Kutta_methods">Runge Kutta methods</a>)**

### A simple example
DyCon Toolbox is a framework to define a optimal control problems in easy way. 

<p>The general formulation of these problems are: </p>

$$
\min_{u\in \Omega} \bigg[ \Psi(x(T)) + \int_0^T L(t,x,u) dt \bigg] \\
\text{subject to:} \ 
\begin{cases}
\dot{x} = f(t,x,u) \\ 
x(0) = x0
\end{cases}
$$

In DyCon toolbox syntax the definition is very similar:
```matlab
>> import casadi.*
>> x = SX.sym('x',[2 1]);
>> u = SX.sym('u',[2 1]);
>> t = SX.sym('t');
>> f = casadi.Function('f',{t,x,u},{x - x.^2 + u});
```
We can define the  `ode` command to build a MATLAB object 
```matlab
>> T  = 2;
>> Nt = 100;
>> tspan = linspace(0,T,Nt);
```
Then we can set the solver and initial condition of the dynamic:

```matlab
>> % Build a ode object
>> idyn = ode(f,x,u,tspan);
>> SetIntegrator(idyn,'RK8')
>> idyn.InitialCondition = [2,4]';
```
Then, With `ocp` command, we can define the optimal control problem in this way:
```matlab
>> psi = casadi.Function('psi' , {x}     , { x.'*x });
>> L   = casadi.Function('L'   , {t,x,u} , { u.'*u });
>> iocp = ocp(idyn,L,psi);
```
Finally, we can solve the problem using IPOPT
```matlab
>> % Choose a control initial guess
>> u0 = ZerosControl(idyn);
>> [uopt,xopt] = IpoptSolver(iocp,u0);
```