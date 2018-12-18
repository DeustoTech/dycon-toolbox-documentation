---
title: ControlParameterDependent
data: 
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
categories: [ documentation , MDL01 , ControlParameterDependent]
class: ControlParameterDependent
layout: method
---
