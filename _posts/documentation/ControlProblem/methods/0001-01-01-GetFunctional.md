---
title: GetFunctional
data: 
  description: Method capable of calculating the value of the functional defined in the control problem.
  little_description: Method capable of calculating the value of the functional defined in the control problem.
  autor: JOroya
  MandatoryInputs:   
   iCP: 
     description:  Control Problem
     class: ControlProblem
     dimension: [1x1]
   Y: 
     name: Solution of ODE
     description: 
     class: ControlProblem
     dimension: [1x1]
   U: 
     name: matrix of control
     description: 
     class: ControlProblem
     dimension: [1x1]
  Outputs:
   JValue:
     name: Functional value with this U and Y 
     description: double 
     class: double
     dimension: [1x1]
categories: [ documentation , MDL01 , ControlProblem]
class: ControlProblem
layout: method
---
