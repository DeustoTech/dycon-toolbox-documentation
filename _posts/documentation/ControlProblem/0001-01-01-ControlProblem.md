---
description: Control Problem Class
title: ControlProblem
categories: [documentation, MDL01]
layout: class
type: constructor
properties:
   Jfun: 
      description: "ControlProblem/Jfun is a property."
      type: "ControlProblem/Jfun is a property."
   ode: 
      description: "ControlProblem/ode is a property."
      type: "ControlProblem/ode is a property."
   T: 
      description: "ControlProblem/T is a property."
      type: "ControlProblem/T is a property."
   dt: 
      description: "ControlProblem/dt is a property."
      type: "ControlProblem/dt is a property."
   UOptimal: 
      description: "ControlProblem/UOptimal is a property."
      type: "ControlProblem/UOptimal is a property."
   precision: 
      description: ""
      type: ""
   P: 
      description: ""
      type: ""
   adjoint: 
      description: ""
      type: ""
   dH_du: 
      description: ""
      type: ""
   Jhistory: 
      description: ""
      type: ""
   yhistory: 
      description: ""
      type: ""
   uhistory: 
      description: ""
      type: ""
   iter: 
      description: ""
      type: ""
   time: 
      description: ""
      type: ""
   dimension: 
      description: ""
      type: ""
methods:
   ControlProblem:
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

# tp8721c4b3_1c18_47c2_94bf_494a95565fd8


Ejemplo de control problem



