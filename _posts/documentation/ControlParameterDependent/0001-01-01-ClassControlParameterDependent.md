---
description: ANA Cambio - The Average Control class is able to calculate the average control given the matrices that depend on the parameter. It has as parameter the state where you want to take all the equations that depend on the parameters.
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
              name: Control Prameter Dependent
              description: Control Prameter Dependent Class
        url: /documentation/MDL01/ControlParameterDependent/ControlParameterDependent
   AverageClassicalGradient:
        description: The Average Control solve an optimal control problem which is constructed to
          control the distance between the average of the states in the last time
          and a given final target. The states are defined via a
          parameter-dependent linear system of differential equations
          $$\dot{x}(t,\nu)=A(\nu)x(t,\nu)+B(\nu)u(t)$$
          The optimum is computed applying different iterative algorithms based
          on gradient descent methods. This function solve a particular optimal control problem using
          the classical gradient descent algorithm. The restriction of the optimization 
          problem is a parameter-dependent finite dimensional linear system. Then, the 
          resulting states depend on a certain parameter. Therefore, the functional is
          constructed to control the average of the states with respect to this parameter.
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
           default:   1e-5
          gamma:
           description: Length Step of the gradient Method. The control is update as follow $$u_{k+1} = u_{k} + \gamma \nabla u_{k}$$
           class: double
           dimension: [1x1]
           default:   1e-1
          MaxIter:
           description: Maximun of iterations of this method
           class: double
           dimension: [1x1]
           default:   100
        url: /documentation/MDL01/ControlParameterDependent/AverageClassicalGradient
   AverageConjugateGradient:
        description: This function solve a particular optimal control problem using
          the stochastic gradient descent algorithm. The restriction of the optimization 
          problem is a parameter-dependent finite dimensional linear system. Then, the 
          resulting states depend on a certain parameter. Therefore, the functional is
          constructed to control the average of the states with respect to this parameter.
          See Also in AverageClassicalGradient
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
           default:   1e-5
          MaxIter:
           description: Maximun of iterations of this method
           class: double
           dimension: [1x1]
           default:   100
        url: /documentation/MDL01/ControlParameterDependent/AverageConjugateGradient
   AverageStochasticGradient:
        description:  This function solve a particular optimal control problem using
          the stochastic gradient descent algorithm. The restriction of the optimization 
          problem is a parameter-dependent finite dimensional linear system. Then, the 
          resulting states depend on a certain parameter. Therefore, the functional is
          constructed to control the average of the states with respect to this parameter.
          See Also in AverageClassicalGradient
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
           default:   1e-5
          gamma0:
           description: Length Step of the gradient Method. The control is update as follow $$u_{k+1} = u_{k} + \gamma \nabla u_{k}$$. In Stochastic method $\gamma_{k} = \gamma_0 * \frac{1}/{\sqrt{k}}$
           class: double
           dimension: [1x1]
           default:   1e-1
          MaxIter:
           description: Maximun of iterations of this method
           class: double
           dimension: [1x1]
           default:   100
        url: /documentation/MDL01/ControlParameterDependent/AverageStochasticGradient
   SimultaneousStochasticGradient:
        description:  This function solve a particular optimal control problem using
          the stochastic gradient descent algorithm. The restriction of the optimization 
          problem is a parameter-dependent finite dimensional linear system. Then, the 
          resulting states depend on a certain parameter. Therefore, the functional is
          constructed to control the average of the states with respect to this parameter.
          See Also in AverageClassicalGradient
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
           default:   1e-5
          gamma0:
           description: Length Step of the gradient Method. The control is update as follow $$u_{k+1} = u_{k} + \gamma \nabla u_{k}$$. In Stochastic method $\gamma_{k} = \gamma_0 * \frac{1}/{\sqrt{k}}$
           class: double
           dimension: [1x1]
           default:   1e-1
          MaxIter:
           description: Maximun of iterations of this method
           class: double
           dimension: [1x1]
           default:   100
        url: /documentation/MDL01/ControlParameterDependent/SimultaneousStochasticGradient
   animation:
        description: This method allows us to see an animation of the evolution of gradient methods, shows the controls in each iteration with a lapse of $dt=0.15s$
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
        url: /documentation/MDL01/ControlParameterDependent/animation
   plot:
        description: The plot function applied to a ControlParameterDepent object shows 
                     three graphs that represent the evolution of the different dimensions 
                     of the state variable, the optimal control that leads the average state 
                     to the desired target, in addition to the convergence of the process.
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
        url: /documentation/MDL01/ControlParameterDependent/plot

---

Average Control Help

