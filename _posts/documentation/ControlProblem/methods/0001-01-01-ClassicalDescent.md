---
title: ClassicalDescent
url: /documentation/MDL01/ControlProblem/ClassicalDescent
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
categories: [ documentation , MDL01 , ControlProblem]
layout: method
---
