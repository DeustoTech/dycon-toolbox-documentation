---
description: The goal of this class is to solve optimal control problems where the states are defined via 
              finite dimensional parameter-dependent systems of the form 
              $$\dot{x}(t,\nu)=A(\nu)x(t,\nu)+B(\nu)u(t), \, t>T, \quad x(0)=x0,$$ 
              being $\nu$ the parameter that can be discrete or continuous. 
              Different iterative algorithms based on gradient descent methods are performed 
              to reach this objective. For example, the classical gradient descent technique or stochastic 
              gradient descent method, which has become important in the last years.   
visible: true
title: ControlParameterDependent
categories: [documentation, MDL01]
layout: class
type: constructor
properties:
   N: 
        type: "Numeric value"
        default: "none"
        description: "Number of states of the system"
      
   A: 
        type: "Matrix"
        default: "none"
        description: $N\times N$ matrix governing the free dynamics of the system
      
   B: 
        type: "Matrix"
        default: "none"
        description: $N\times M$ matrix. Control operator
      
   x0: 
        type: "Vector"
        default: "none"
        description: "Vector with the initial states"
      
   u0: 
        type: "Vector"
        default: "none"
        description: "Vector dimension initial value of the control"
      
   span: 
        type: "Vector"
        default: "none"
        description: "Vector of time"
      
   K: 
        type: "Numerical value"
        default: "none"
        description: Length of the parameter $\nu$
      
   addata: 
        type: "Numerical value"
        default: "none"
        description: "Aditional data of gradient methods. You can find the history "
      
   u: 
        type: "Numerical value"
        default: "none"
        description: "Control Obtain"
      
methods:
   ControlParameterDependent:
        name: ControlParameterDependent
        description: ControlParameterDependent constructor
        autor: JOroya
        MandatoryInputs:   
          iode: 
              name: Ordinary Differential Equation 
              description: Ordinary Differential Equation represent the
                  constrain to minimize the functional. It is a finite
                  dimensional parameter-dependent linear system of ordinary
                  differential equations."
              class: ode
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
              description: "This parameter represent is the interval to interpolate the control u and state y to obtain the functional"
              class: double
              dimension: [1x1]
              default: iode.dt 
        Outputs:
          obj:
              description: Control Prameter Dependent Class
        url: /documentation/mdl01/ControlParameterDependent/ControlParameterDependent
   AverageClassicalGradient:
        description: The Average Classical Gradient solves an optimal control problem 
              which is constructed to control the distance between the average of the states in the last time
              and a given final target. This function solve a particular optimal control problem using
              the classical gradient descent algorithm. The restriction of the optimization 
              problem is a parameter-dependent finite dimensional linear system. Then, the 
              resulting states depend on a certain parameter. Hence, the functional is
              constructed to control the average of the states with respect to this parameter
              $$ \frac{1}{\vert \mathcal{K} \vert} \sum_{\nu \in \mathcal{K}}x(T,\nu) = xt  $$.
        little_description: The Average Classical Gradient solves an optimal control problem 
        autor: AnaN
        MandatoryInputs:   
          iCPD: 
           description: Control Parameter Dependent Problem 
           class: ControlParameterDependent
           dimension: [1x1]
          xt: 
           description: The final target. The system will be controlled to starting in x0 ending in xt.
           class: double
           dimension: [iCPD.Nx1]
        OptionalInputs:
          tol:
           description: tolerance of algorithm, this number is compare with the
                          following error in order to stop the algorithm
                          $$\frac{\vert \vert u_{k+1}-u_{k}\vert \vert}{\vert \vert u_{k+1}\vert
                          \vert}$$
           class: double
           dimension: [1x1]
           default:   1e-5
          beta:
           description: This value is applied to regularize the control in the optimal control problem
                          $$ \min_{u \in L^2(0,T)} J(u)=\frac{1}{2} \left( \frac{1}{|\mathcal{K}|} \sum_{\nu \in \mathcal{K}} x \left( T, \nu \right) - xt \right)^2  + \frac{\beta}{2} \int_0^T u^2 \mathrm{d}t, \quad \beta \in \mathbb{R}^+ $$ 
           class: double
           dimension: [1x1]
           default:   1e-1
          gamma0:
           description: Initial step of the method. The control is update as follow
                          $$u_{k+1} = u_{k} + \gamma_{k} \nabla J(u_{k}),$$
                          where $\gamma_{k} = \gamma_0 * \frac{1}/{\sqrt{k}}$
           class: double
           dimension: [1x1]
           default:   0.5
          MaxIter:
           description: Maximun of iterations of this method
           class: double
           dimension: [1x1]
           default:   1000
        url: /documentation/mdl01/ControlParameterDependent/AverageClassicalGradient
   AverageConjugateGradient:
        description: The Average Conjugate Gradient solves an optimal control problem 
                      which is constructed to control the distance between the average of the states in the last time
                      and a given final target. This function solve a particular optimal control problem using
                      the classical gradient descent algorithm. The restriction of the optimization 
                      problem is a parameter-dependent finite dimensional linear system. Then, the 
                      resulting states depend on a certain parameter. 
                      See Also in AverageClassicalGradient
        little_description: This function solve a particular optimal control problem using
                          the Conjugate gradient descent algorithm.
        autor: AnaN
        MandatoryInputs:   
          iCPD: 
           description: Control Parameter Dependent Problem 
           class: ControlParameterDependent
           dimension: [1x1]
          xt: 
           description: The target vector where you want the system to go
           class: double
           dimension: [iCPD.Nx1]
        OptionalInputs:
          tol:
           description: tolerance of algorithm, this number is compare with $J(k)-J(k-1)$
           class: double
           dimension: [1x1]
           default:   1e-5
          beta:
           description: This number is the power of the control, is define by follow expresion $$J = \min_{u \in L^2(0,T)} \frac{1}{2} \left[ \frac{1}{|\mathcal{K}|} \sum_{\nu \in \mathcal{K}} x \left( T, \nu \right) - \bar{x} \right]^2  + \frac{\beta}{2} \int_0^T u^2 \mathrm{d}t, \quad \beta \in \mathbb{R}^+ $$ 
           class: double
           dimension: [1x1]
           default:   1e-1
          MaxIter:
           description: Maximun of iterations of this method
           class: double
           dimension: [1x1]
           default:   100
        url: /documentation/mdl01/ControlParameterDependent/AverageConjugateGradient
   AverageStochasticGradient:
        description:  This function solves a particular optimal control problem using
                      the stochastic gradient descent algorithm. The restriction of the optimization 
                      problem is a parameter-dependent finite dimensional linear system. Then, the 
                      resulting states depend on a certain parameter. Hence, the functional is
                      constructed to control the average of the states with respect to this parameter
                      $$ \frac{1}{\vert \mathcal{K} \vert} \sum_{\nu \in \mathcal{K}}x(T,\nu) = xt  $$
                      See Also in AverageClassicalGradient
        little_description: This function solves a particular optimal control problem using
                              the stochastic gradient descent algorithm.
        autor: AnaN
        MandatoryInputs:   
          iCPD: 
           description: Control Parameter Dependent Problem 
           class: ControlParameterDependent
           dimension: [1x1]
          xt: 
           description: The final target. The system will be controlled to starting in x0 ending in xt.
           class: double
           dimension: [iCPD.Nx1]
        OptionalInputs:
          tol:
           description: tolerance of algorithm, this number is compare with the
                          following error in order to stop the algorithm
                          $$\frac{\vert \vert u_{k+1}-u_{k}\vert \vert}{\vert \vert u_{k+1}\vert
                          \vert}$$
           class: double
           dimension: [1x1]
           default:   1e-5
          beta:
           description: This value is applied to regularize the control in the optimal control problem
                          $$ \min_{u \in L^2(0,T)} J(u)=\frac{1}{2} \left( \frac{1}{|\mathcal{K}|} \sum_{\nu \in \mathcal{K}} x \left( T, \nu \right) - xt \right)^2  + \frac{\beta}{2} \int_0^T u^2 \mathrm{d}t, \quad \beta \in \mathbb{R}^+ $$ 
           class: double
           dimension: [1x1]
           default:   1e-1
          gamma0:
           description: Initial step of the method. The control is update as follow
                          $$u_{k+1} = u_{k} + \gamma_{k} \nabla J_{i_{k}}(u_{k})(u_{k}),$$
                          where $\gamma_{k} = \gamma_0 * \frac{1}/{\sqrt{k}}$
           class: double
           dimension: [1x1]
           default:   0.5
          MaxIter:
           description: Maximun of iterations of this method
           class: double
           dimension: [1x1]
           default:   1000
        url: /documentation/mdl01/ControlParameterDependent/AverageStochasticGradient
   animation:
        description: This method allows us to see an animation of the evolution of gradient methods, shows the controls
                          in each iteration with a lapse of $dt=0.15s$
        little_description: This method allows us to see an animation of the evolution of gradient methods, 
                              shows the controls in each iteration with a lapse of $dt=0.15s$
        autor: JOroya
        MandatoryInputs:   
         iCPD: 
           description: Control Parameter Dependent Problem
           class: ControlParameterDependent
           dimension: [1x1]
        OptionalInputs:
          figure: 
           description: figure where is the animation
           class: figure
           dimension: [1x1]
           default: []
          XLim: 
           description: axes YLim of Vector State 
           class: double
           dimension: [1x2]
           default: []
          ULim: 
           description: axes YLim of Vector Control 
           class: double
           dimension: [1x2]
           default: []
          JLim: 
           description: axes YLim of Functional Convergence 
           class: double
           dimension: [1x2]
           default: []
          SaveGif: 
           description: if this option is true, so the animation is save in gif format
           class: boolean
           dimension: [1x1]
           default: false
          path: 
           description: Name of file where the Gif will be saved
           class: string
           dimension: [1x1]
           default: ' '
          dt: 
           description: Interval of time between capture 
           class: double
           dimension: [1x1]
           default: 0.15
        url: /documentation/mdl01/ControlParameterDependent/animation
   plot:
        description: The plot function applied to a ControlParameterDepent object shows 
                     three graphs that represent the evolution of the different dimensions 
                     of the state variable, the optimal control that leads the average state 
                     to the desired target, in addition to the convergence of the process.
        little_description: The plot function applied to a ControlParameterDepent object shows  the evolution of optimization
        autor: JOroya
        MandatoryInputs:   
          iAverageProblem: 
           name: ControlParameterDependent object
           description: Main object of ControlParameterDependent
           class: ControlProblem
           dimension: [1x1]
        OptionalInputs:
          U0:
           name: Initial Control 
           description: matrix 
           class: double
           dimension: [length(iCP.tline)]
           default:   empty
        url: /documentation/mdl01/ControlParameterDependent/plot
   SimultaneousClassicalGradient:
        description:  The Simultaneous Classical Gradient solves an optimal control problem 
                      which is constructed to control each statein the last time
                      and a given final target. This function solve a particular optimal control problem using
                      the classical gradient descent algorithm. The restriction of the optimization 
                      problem is a parameter-dependent finite dimensional linear system. Then, the 
                      resulting states depend on a certain parameter. Hence, the functional is
                      constructed to control each state with respect to this parameter
                      $$ x(T,\nu) = xt \quad \forall \nu \in \mathcal{K}  $$.
                      See Also in AverageClassicalGradient
        little_description: The Simultaneous Classical Gradient solves an optimal control problem 
                              which is constructed to control each statein the last time
                              and a given final target.
        autor: AnaN
        MandatoryInputs:   
          iCPD: 
           description: Control Parameter Dependent Problem 
           class: ControlParameterDependent
           dimension: [1x1]
          xt: 
           description: The final target. The system will be controlled to starting in x0 ending in xt.
           class: double
           dimension: [iCPD.Nx1]
        OptionalInputs:
          tol:
           description:  tolerance of algorithm, this number is compare with the
                          following error in order to stop the algorithm
                          $$\frac{\vert \vert u_{k+1}-u_{k}\vert \vert}{\vert \vert u_{k+1}\vert
                          \vert}$$
           class: double
           dimension: [1x1]
           default:   1e-5
          beta:
           description: This value is applied to regularize the control in the optimal control problem
                          $$ \min_{u \in L^2(0,T)} J(u)=\frac{1}{2}  \frac{1}{|\mathcal{K}|} \sum_{\nu \in \mathcal{K}}\left( x \left( T, \nu \right) - xt \right)^2  + \frac{\beta}{2} \int_0^T u^2 \mathrm{d}t, \quad \beta \in \mathbb{R}^+ $$ 
           class: double
           dimension: [1x1]
           default:   1e-1
          gamma0:
           description: Initial step of the method. The control is update as follow
                          $$u_{k+1} = u_{k} + \gamma_{k} \nabla J(u_{k}),$$
                          where $\gamma_{k} = \gamma_0 * \frac{1}/{\sqrt{k}}$
           class: double
           dimension: [1x1]
           default:   0.5
          MaxIter:
           description: Maximun of iterations of this method
           class: double
           dimension: [1x1]
           default:   1000
        url: /documentation/mdl01/ControlParameterDependent/SimultaneousClassicalGradient
   SimultaneousStochasticGradient:
        description:  The Simultaneous Stochastic Gradient solves an optimal control problem 
                  which is constructed to control each statein the last time
                  and a given final target. This function solve a particular optimal control problem using
                  the classical gradient descent algorithm. The restriction of the optimization 
                  problem is a parameter-dependent finite dimensional linear system. Then, the 
                  resulting states depend on a certain parameter. Hence, the functional is
                  constructed to control each state with respect to this parameter
                  $$ x(T,\nu) = xt \quad \forall \nu \in \mathcal{K}  $$.
        little_description: The Simultaneous Stochastic Gradient solves an optimal control problem 
                      which is constructed to control each statein the last time
                       and a given final target.
        autor: AnaN
        MandatoryInputs:   
          iCPD: 
           description: Control Parameter Dependent Problem 
           class: ControlParameterDependent
           dimension: [1x1]
          xt: 
           description: The final target. The system will be controlled to starting in x0 ending in xt.
           class: double
           dimension: [iCPD.Nx1]
        OptionalInputs:
          tol:
           description: tolerance of algorithm, this number is compare with the
                          following error in order to stop the algorithm
                          $$\frac{\vert \vert u_{k+1}-u_{k}\vert \vert}{\vert \vert u_{k+1}\vert
                          \vert}$$
           class: double
           dimension: [1x1]
           default:   1e-5
          beta:
           description: This value is applied to regularize the control in the optimal control problem
                          $$ \min_{u \in L^2(0,T)} J(u)=\frac{1}{2}  \frac{1}{|\mathcal{K}|} \sum_{\nu \in \mathcal{K}}\left( x \left( T, \nu \right) - xt \right)^2  + \frac{\beta}{2} \int_0^T u^2 \mathrm{d}t, \quad \beta \in \mathbb{R}^+ $$ 
           class: double
           dimension: [1x1]
           default:   1e-1
          gamma0:
           description: Initial step of the method. The control is update as follow
                          $$u_{k+1} = u_{k} + \gamma_{k} \nabla J(u_{k}),$$
                           where $\gamma_{k} = \gamma_0 * \frac{1}/{\sqrt{k}}$
           class: double
           dimension: [1x1]
           default:   0.5
          MaxIter:
           description: Maximun of iterations of this method
           class: double
           dimension: [1x1]
           default:   1000
        url: /documentation/mdl01/ControlParameterDependent/SimultaneousStochasticGradient

---

The optimal control of the following functional is obtained applying the classical gradient descent algorithm


$$ \begin{equation*} \min_{u \in L^2(0,T)} \mathcal{J}\left( u\right) = \min_{u \in L^2(0,T)} \frac{1}{2} \left[ \frac{1}{|\mathcal{K}|} \sum_{\nu \in \mathcal{K}} x \left( T, \nu \right) - \bar{x} \right]^2  + \frac{\beta}{2} \int_0^T u^2 \mathrm{d}t, \quad \beta \in \mathbb{R}^+ \end{equation*} $$


Subject to the finite dimensional linear control system mentioned before, the goal is to apply the stochastic gradient descent method to obtain the minimun of the same optimal control problem.


In this case, the iterative method is defined as


$$\begin{equation*} u^{\left( k+1 \right)} = u^{\left( k \right)} - \gamma \left( \beta u^{\left( k \right)}- B^{\top}p \left( t,\nu_{i_k} \right) \right), \end{equation*} $$


where $p \left( t,\nu_{i_k} \right)$ is solution of the following adjoint problem


$$ \begin{align*} \left\{ \begin{array}{ll} p^\prime \left( t, \nu \right) = -A \left( \nu \right) p \left( t,\nu \right), \quad 0 < t <T, \\ \displaystyle p\left( T \right) = - \left[ \frac{1}{|\mathcal{K}|} \sum_{\nu \in \mathcal{K}} x \left( T, \nu \right) - \bar{x} \right]. \end{array} \right. \end{align*} $$


The values of parameter $\nu_i$ are

```matlab
nu = 1:1:5;
```


And save in K, the number of values

```matlab
K = length(nu);
```


We can, define the initial state of all ODE's

```matlab
N = 2; % dimension of vector state
x0 = ones(N, 1);
```


We take as final target

```matlab
xt = [0.5;0];
```


Also, we need to define a initial control, that will be evolve

```matlab
dt = 0.02; t0 = 0; T  = 1; span = (t0:dt:T);
%
u0 = zeros(length(span),1);
```


Moreover, we can define the matrix A's and B's, that determine the linear system

```matlab
Am = -triu(ones(N));
```

```matlab
Bm = zeros(N, 1);
Bm(N) = 1;
```

```matlab
A = zeros(N,N,K);
B = zeros(N,1,K);
for index = 1:K
    A(:,:,index) = Am + (nu(index) - 1 )*diag(diag(Am));
    B(:,:,index) = Bm;
end
```


Then, we solve the problem applying the stochastic gradient descent algorithm

```matlab
AverageProblemSG = ControlParameterDependent(A,B,x0,u0,span);
```

```matlab
AverageStochasticGradient(AverageProblemSG,xt)
```


You can see the results

```matlab
plot(AverageProblemSG)
```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/MDL01/class/main/ControlParameterDependent/copiaRM_01.png)

