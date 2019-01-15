---
description: LinearControl is a subclass of the ControlProblem class, so it is also a control problem. 
              However, we assume that the differential equation we want to control is linear. This gives 
              us access to new functions such as the conjugate gradient. In addition, it lightens the 
              computational cost and some functions such as GetAdjointProblem.
visible: true
title: LinearControl
number: 1
categories: [documentation, MDL01]
layout: class
type: constructor
properties:
   gramian: 
        type: double
        default: none
        description: Gramian Matrix
      
   ss: 
        type: double
        default: space
        description: MATLAB class that represent de dynamics
      
methods:
   LinearControl:
        name: ControlProblem
        description: 
        autor: JOroya
        MandatoryInputs:   
          iode: 
              name: Linear Ordinary Differential Equation 
              description: Ordinary Differential Equation represent the constrain to minimization the functional 
              class: LinearODE
              dimension: [1x1]
          Jfun: 
              name: functional
              description: Cost function to obtain the optimal control 
              class: Functional
              dimension: [1x1]        
        OptionalInputs:
          T:
              name: Final Time 
              description: This parameter represent the final time of simulation.  
              class: double
              dimension: [1x1]
              default: iode.T 
          dt:
              name: Final Time 
              description: This parameter represent is the interval to interpolate the control, $u$, and state, $y$, to obtain the functional $J$ and the gradient $dH/du$
              class: double
              dimension: [1x1]
              default: iode.dt         
        Outputs:
          obj:
              name: ControlProblem MATLAB
              description: ControlProblem MATLAB class
              class: ControlProblem
              dimension: [1x1]
        url: /documentation/mdl01/LinearControl/LinearControl
   ConjugateGradientDescent:
         description: This method is able to update the value of the control by decreasing 
                      the value of the functional. By calculating the congugate gradient, $ \frac{dH}{du}$.
         little_description: This method is able to update the value of the control by decreasing 
                      the value of the functional.
         autor: UmbertoB
         MandatoryInputs:   
           iCP: 
               description: Control Problem Object
               class: ControlProblem
               dimension: [1x1]
           UOld: 
               description: Control Vector in time  
               class: double
               dimension: [M,iCP.tline]
           YOld: 
               description: State Vector in time 
               class: double
               dimension: [length(iCP.ode.Y0),iCP.tline]
           JOld: 
               description: Value of functional J(Uold,Yold)
               class: double
               dimension: [length(iCP.ode.Y0),iCP.tline]
         Outputs:
           Unew:
               description: Update of Control Vector  
               class: double
               dimension: [Mxlength(iCP.tline)]
           Ynew:
               description: Update of State Vector 
               class: double
               dimension: [length(iCP.tline)]
           Jnew:
               description: New Value of functional 
               class: double
               dimension: [1x1]
         url: /documentation/mdl01/LinearControl/ConjugateGradientDescent
   GetAdjointProblem:
        description: This method adds the problem adjoint to the Control Problem object, since we have
                      $$ \dot{\textbf{Y}} = f(\textbf{Y},t) $$ 
                      and the functional
                      $$ J = \Psi(\textbf{Y}(T)) + \int_{0}^T L(\textbf{Y},U,t)dt $$ 
                      we can create the Hamiltonian 
                      $$ H = L + P*F $$
                      where $\textbf{P} = [p_1 p_2 p_3 ... ]^T$ . So according to the principle of the maximum of pontriagin,
                      we can calculate the attached problems through the formulas
                      $$ \frac{d\textbf{P}}{dt} = \vec{\nabla}_{Y} H = 
                      (\frac{\partial H}{ \partial y_1},\frac{\partial H}{ \partial y_2},...)$$
                      with the final time condition
                      $$ \textbf{P}(T) = 
                      (\frac{\partial \Psi}{ \partial y_1},\frac{\partial \Psi}{ \partial y_2},...)$$
        little_description: Method capable of obtaining the attached problem and its final condition.
        autor: JOroya
        MandatoryInputs:   
           iCP: 
               name: Control Problem
               description: Control problem object
               class: ControlProblem
               dimension: [1x1]
        url: /documentation/mdl01/LinearControl/GetAdjointProblem

---

First define the vectors


$$ symY = \left( \begin{matrix}   y1 \\                                   y2                  \end{matrix} \right)    symU = \left( \begin{matrix}   u1 \\                                   u2                   \end{matrix} \right) $$


We will use symbolic variables to define them.

```matlab
syms t
symY = SymsVector('y',2);
symU = SymsVector('u',2);
```


**Ordinary differential equation**


In this case we will define the following differential equation


$$ \dot{\textbf{Y}} = \left( \begin{matrix}   -1  &  1 \\    0  & -2 \\   \end{matrix} \right) * \textbf{Y} +   \left( \begin{matrix}    1  &  0 \\    0  &  1 \\   \end{matrix} \right) * \textbf{U} $$

```matlab
A = [ -1  1  ; 0 -2 ];
B = [  1  0  ; 0  1 ];
```


To do this, we create an object differential equation. We can do it with the ODE constructor, in the following way.

```matlab
odeEqn = LinearODE(A,B);
Y0 = [  0;1 ];
odeEqn.Y0 = Y0;
```


**Cost Functional**


$$ J = \Psi(Y(T),t) + \int_0^T L(Y(t,U),U(t),t) dt$$


For this, we choose a target of vector state

```matlab
YT = [ 1; 4];
```


Then,


$$\Psi(Y,t) = \vert Y(T) - Y(t) \vert ^2 $$


$$ L(Y(t,U),U(t),t) = \beta \vert U(t) \vert^2$$

```matlab
symPsi  = (YT - symY).'*(YT - symY);
symL    = 0.0001*(symU.'*symU);
```


For last, you an create the functional object

```matlab
Jfun = Functional(symPsi,symL,symY,symU);
```


Now, We can create the control problem

```matlab
iCP1 = LinearControl(odeEqn,Jfun);
```


and solve by Classical Gradient Method

```matlab
GradientMethod(iCP1)
```


Solve the equation without control

```matlab
solve(odeEqn)
plot(odeEqn)
```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/MDL01/class/main/LinearControl/copiaRM_01.png)

And compare the controlled solution

```matlab
plot(iCP1.ode)
```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/MDL01/class/main/LinearControl/copiaRM_02.png)

