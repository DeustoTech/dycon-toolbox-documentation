---
data:
  description: Compute the rigidity matrix for solving the Poisson problem
                    $$(-\Delta)^s u = F  \ \in (-L,L)$$
                    where $u=0, \in R(-L,L)$ using linear finite elements on a mesh of N points
  autor: UmbertoB
  MandatoryInputs:   
    s: 
        name: fractrio
        d: [1x1]
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
    A:
        name: Mass Matrix of Fractional Laplacian
        description: Mass Matrix of Fractional Laplacian
        dimension: [NxN]
        class:  double

title: FractionalLaplacian
categories: [documentation, MDL02]
layout: function
helpfile: /Users/jesusoroya/Documents/GitHub/DyCon-Computational-Platform/helps/MDL02_FiniteElement/functions
---

Ejemplo de Fractional

