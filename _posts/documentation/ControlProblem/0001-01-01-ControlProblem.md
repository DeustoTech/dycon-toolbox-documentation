---
description: The problem control class is able to solve problems of optimization of a function restricted to an ordinary differential equation. This scheme is used to solve optimal control problems in which the functional derivative is calculated. This class has methods that help us find optimal control as well as the obtaining of the attached problem and the form of the derivative, in its symbolic and numerical versions.
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
              description: 'This parameter represent is the interval to interpolate the control u and state y to obtain the functional J and the gradient dH/du'
              class: double
              dimension: [1x1]
              default: iode.dt
   GetAdjointProblem:
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
         Output:
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
---

Ejemplo de control problem

