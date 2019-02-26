---
title: CoGradientMethod
data: 
  name: GradientMethod
  little_description: The gradient method is able to optimize the given functional, going down the gradient.
  description: "The gradient method is able to optimize the given
                        functional, going down the gradient. El calculo del gradiente puede
                        ser de varios tipo. Por defecto la direccion y el modulo de descenso
                        se calcula con el gradiente conjugado
                        http://web.mit.edu/mitter/www/publications/2_conjugate_grad_IEEEAC.pdf"
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
        dimension: [length(iCP.tspan)]
        default: zeros
    MaxIter:
        name: Initial Control 
        description: matrix 
        class: double
        dimension: [1x1]
        default: 50
    tol:
        name: Initial Control 
        description: matrix 
        class: double
        dimension: 
        dimension: [1x1]
    DescentParameters:
        description: Parmater of Descent Method 
        class: double
        dimension: cell
        default: cell.empty    
    Graphs:
        description: Parameter that indicate if the method must plot the optimization, while is calculate 
        class: logical
        dimension: [1x1]
        default: false        
    TypeGraphs:
        description: Type of graphs. This parameter can be 'ODE' or 'PDE' 
        class: string
        dimension: [1x1]
        default: 'ODE'
    SaveGif:
        name: If this parameter is true, A gif of the optimization process is created
        description: matrix 
        class: double
        dimension: [length(iCP.tspan)]
        default: false
    restart:
        description: The optimization start with U0 = iCP.UOptimal
        class: double
        dimension: [1x1]
        default: false
categories: [ documentation , MDL01 , OptimalControl]
class: OptimalControl
layout: method
---
