---
title: ControlProblem
data: 
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
categories: [ documentation , MDL01 , ControlProblem]
class: ControlProblem
layout: method
---
