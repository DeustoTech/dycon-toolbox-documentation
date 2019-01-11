---
title: AverageConjugateGradient
data: 
  description: The Average Conjugate Gradient solves an optimal control problem 
                which is constructed to control the distance between the average of the states in the last time
                and a given final target. This function solve a particular optimal control problem using
                the classical gradient descent algorithm. The restriction of the optimization 
                problem is a parameter-dependent finite dimensional linear system. Then, the 
                resulting states depend on a certain parameter. 
                See Also in AverageClassicalGradient
  little_description: This function solve a particular optimal control problem using
                    the Conjugate gradient descent algorithm.
  autor: AnaN
  MandatoryInputs:   
    iCPD: 
     description: Control Parameter Dependent Problem 
     class: ControlParameterDependent
     dimension: [1x1]
    xt: 
     description: The target vector where you want the system to go
     class: double
     dimension: [iCPD.Nx1]
  OptionalInputs:
    tol:
     description: tolerance of algorithm, this number is compare with $J(k)-J(k-1)$
     class: double
     dimension: [1x1]
     default:   1e-5
    beta:
     description: This number is the power of the control, is define by follow expresion $$J = \min_{u \in L^2(0,T)} \frac{1}{2} \left[ \frac{1}{|\mathcal{K}|} \sum_{\nu \in \mathcal{K}} x \left( T, \nu \right) - \bar{x} \right]^2  + \frac{\beta}{2} \int_0^T u^2 \mathrm{d}t, \quad \beta \in \mathbb{R}^+ $$ 
     class: double
     dimension: [1x1]
     default:   1e-1
    MaxIter:
     description: Maximun of iterations of this method
     class: double
     dimension: [1x1]
     default:   100
categories: [ documentation , MDL01 , ControlParameterDependent]
class: ControlParameterDependent
layout: method
---
