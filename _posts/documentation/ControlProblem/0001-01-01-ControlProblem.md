---
description: This class is able to solve optimization problems of a function restricted to an ordinary differential equation. This scheme is used to solve optimal control problems in which the functional derivative is calculated. <strong>ControlProblem</strong> class has methods that help us find optimal control as well as obtaining the attached problem and it's derivative form, in both symbolic and numerical versions.
title: ControlProblem
categories: [documentation, MDL01]
layout: class
type: constructor
properties:
   Jfun: 
      type: "Functional"
      default: "none"
      description: "This property represent the cost of optimal control"
   ode: 
      type: "ode"
      default: "none"
      description: "This property represent ordinal differential equation"
   T: 
      type: double
      default: 1
      description: Final Time
   dt: 
   UOptimal: 
   precision: 
   P: 
   adjoint: 
   dH_du: 
   Jhistory: 
   yhistory: 
   uhistory: 
   iter: 
   time: 
   dimension: 
methods:
   ControlProblem:
        name: ControlProblem
        description: 
        autor: JOroya
        MandatoryInputs:   
          iode: 
              name: Ordinary Differential Equation 
              description: Ordinary Differential Equation represent the constrain to minimization the functional 
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
              description: "This parameter represent is the interval to interpolate the control u and state y to obtain the functional J and the gradient dH/du"
              class: double
              dimension: [1x1]
              default: iode.dt         
        Outputs:
          obj:
              name: ControlProblem MATLAB
              description: ControlProblem MATLAB class
              class: ControlProblem
              dimension: [1x1]
        url: /documentation/MDL01/ControlProblem-ControlProblem
   ClassicalDescent:
         description: Metodo de Es
         autor: JOroya
         MandatoryInputs:   
           iCP: 
               name: Control Problem
               description: 
               class: ControlProblem
               dimension: [1x1]
         OptionalInputs:
           U0:
               name: Initial Control 
               description: matrix 
               class: double
               dimension: [length(iCP.tline)]
               default:
         Outputs:
          Unew:
               name: Initial Control 
               description: matrix 
               class: double
               dimension: [length(iCP.tline)]
               default:
          Ynew:
               name: Initial Control 
               description: matrix 
               class: double
               dimension: [length(iCP.tline)]
               default:
          Jnew:
               name: Initial Control 
               description: matrix 
               class: double
               dimension: [length(iCP.tline)]
               default: 
         url: /documentation/MDL01/ControlProblem-ClassicalDescent
   GetAdjointProblem:
        little_description: Metodo capaz de calcular el problema adjunto de la ecuacion diferencial atravez del hamiltoniano
                             asociado (Principi de Pontriagin). Mediante la formula $ \frac{d\textbf{P}}{dt} = \vec{\nabla}_{Y} H $
        description: Este metodo agrega el problema adjunto al objecto ControlProblem, dado que tenemos 
                      $$ \dot{\textbf{Y}} = f(\textbf{Y},t) $$ 
                      y el funcional 
                      $$ J = \Psi(\textbf{Y}(T)) + \int_{0}^T L(\textbf{Y},U,t)dt $$ 
                      podemos crear el Hamiltoniano 
                      $$ H = L + P*F $$
                      donde $\textbf{P} = [p_1 p_2 p_3 ... ]^T$ . Entonces 
                      segun el principio del maximo de pontriagin 
                      podemos calcular el problemas adjunto mediantes las formulas 
                      $$ \frac{d\textbf{P}}{dt} = \vec{\nabla}_{Y} H = 
                      (\frac{\partial H}{ \partial y_1},\frac{\partial H}{ \partial y_2},...)$$
                      con la condicion final 
                      $$ \textbf{P}(T) = 
                      (\frac{\partial \Psi}{ \partial y_1},\frac{\partial \Psi}{ \partial y_2},...)$$
        autor: JOroya
        MandatoryInputs:   
           iCP: 
               name: Control Problem
               description: Control problem object
               class: ControlProblem
               dimension: [1x1]
        Outputs:
           iCP: 
               name: Control Problem
               description: Control problem object
               class: ControlProblem
               dimension: [1x1]
        url: /documentation/MDL01/ControlProblem-GetAdjointProblem
   GetFunctional:
        description: Metodo de Es
        autor: JOroya
        MandatoryInputs:   
        iCP: 
           name: Control Problem
           description: 
           class: ControlProblem
           dimension: [1x1]
        OptionalInputs:
        U0:
           name: Initial Control 
           description: matrix 
           class: double
           dimension: [length(iCP.tline)]
           default:   empty
        url: /documentation/MDL01/ControlProblem-GetFunctional
   GetGradient:
        description: Metodo de Es
        autor: JOroya
        MandatoryInputs:   
        iCP: 
           name: Control Problem
           description: 
           class: ControlProblem
           dimension: [1x1]
        OptionalInputs:
        U0:
           name: Initial Control 
           description: matrix 
           class: double
           dimension: [length(iCP.tline)]
           default:   empty
        url: /documentation/MDL01/ControlProblem-GetGradient
   GradientMethod:
        name: GradientMethod
        description: Metodo de Es
        autor: JOroya
        MandatoryInputs:   
          iCP: 
              name: Control Problem
              description: 
              class: ControlProblem
              dimension: [1x1]
        OptionalInputs:
          U0:
              name: Initial Control 
              description: matrix 
              class: double
              dimension: [length(iCP.tline)]
              default:
        url: /documentation/MDL01/ControlProblem-GradientMethod

---

Ejemplo de control problem

