---
title: GetFunctional
data: 
  description: Metodo de Es
  autor: Xinlung
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
  Outputs:
   U0:
     name: Initial Control 
     description: matrix 
     class: double
     dimension: [length(iCP.tline)]
     default:   empty
categories: [ documentation , MDL01 , ControlProblem]
class: ControlProblem
layout: method
---
