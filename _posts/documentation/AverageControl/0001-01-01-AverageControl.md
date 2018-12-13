---
description: The Average Control class is able to calculate the average control given the matrices that depend on the parameter. It has as parameter the state where you want to take all the equations that depend on the parameters.
title: AverageControl
categories: [documentation, MDL01]
layout: class
type: constructor
properties:
   A: 
      type: "Functional"
      default: "none"
      description: "This property represent the cost of optimal control"
   B: 
      type: "Functional"
      default: "none"
      description: "This property represent the cost of optimal control"
   x0: 
      type: "Functional"
      default: "none"
      description: "This property represent the cost of optimal control"
   u0: 
      type: "Functional"
      default: "none"
      description: "This property represent the cost of optimal control"
   span: 
      type: "Functional"
      default: "none"
      description: "This property represent the cost of optimal control"
   K: 
      type: "Functional"
      default: "none"
      description: "This property represent the cost of optimal control"
   N: 
      type: "Functional"
      default: "none"
      description: "This property represent the cost of optimal control"
   addata: 
   u: 
methods:
   AverageControl:
        name: AverageControl
        description: AverageControl constructor
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
              description: "This parameter represent is the interval to interpolate the control u and state y to obtain the functional"
              class: double
              dimension: [1x1]
              default: iode.dt
   animation:
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
   plot:
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
   solveClassicalGradient:
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
   solveConjugateGradient:
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
   solveStochasticGradient:
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

---

Average Control Help

