---
title: GetFunctional
url: /documentation/MDL01/ControlProblem-GetFunctional
data: 
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
categories: [ documentation ,MDL01,]
layout: method
---