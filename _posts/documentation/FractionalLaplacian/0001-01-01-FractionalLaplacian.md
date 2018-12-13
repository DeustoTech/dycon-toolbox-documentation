---
data:
  description: Compute the rigidity matrix for solving the Poisson problem
                    $$(-\Delta)^s u = F  \ \in (-L,L)$$
                    $$u=0,              \   \in R(-L,L)$$
                    using linear finite elements on a mesh of N points
  autor: UmbertoB
  MandatoryInputs:   
    iCP: 
        name: Control Problem Object
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

---

Ejemplo de Fractional

