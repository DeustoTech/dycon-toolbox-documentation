---
title: AverageStochasticGradient
data: 
  description:  This function solves a particular optimal control problem using
                the stochastic gradient descent algorithm. The restriction of the optimization 
                problem is a parameter-dependent finite dimensional linear system. Then, the 
                resulting states depend on a certain parameter. Hence, the functional is
                constructed to control the average of the states with respect to this parameter
                $$ \frac{1}{\vert \mathcal{K} \vert} \sum_{\nu \in \mathcal{K}}x(T,\nu) = xt  $$
                See Also in AverageClassicalGradient
  little_description: This function solves a particular optimal control problem using
                        the stochastic gradient descent algorithm.
  autor: AnaN
  MandatoryInputs:   
    iCPD: 
     description: Control Parameter Dependent Problem 
     class: ControlParameterDependent
     dimension: [1x1]
    xt: 
     description: The final target. The system will be controlled to starting in x0 ending in xt.
     class: double
     dimension: [iCPD.Nx1]
  OptionalInputs:
    tol:
     description: tolerance of algorithm, this number is compare with the
                    following error in order to stop the algorithm
                    $$\frac{\vert \vert u_{k+1}-u_{k}\vert \vert}{\vert \vert u_{k+1}\vert
                    \vert}$$
     class: double
     dimension: [1x1]
     default:   1e-5
    beta:
     description: This value is applied to regularize the control in the optimal control problem
                    $$ \min_{u \in L^2(0,T)} J(u)=\frac{1}{2} \left( \frac{1}{|\mathcal{K}|} \sum_{\nu \in \mathcal{K}} x \left( T, \nu \right) - xt \right)^2  + \frac{\beta}{2} \int_0^T u^2 \mathrm{d}t, \quad \beta \in \mathbb{R}^+ $$ 
     class: double
     dimension: [1x1]
     default:   1e-1
    gamma0:
     description: Initial step of the method. The control is update as follow
                    $$u_{k+1} = u_{k} + \gamma_{k} \nabla J_{i_{k}}(u_{k})(u_{k}),$$
                    where $\gamma_{k} = \gamma_0 * \frac{1}/{\sqrt{k}}$
     class: double
     dimension: [1x1]
     default:   0.5
    MaxIter:
     description: Maximun of iterations of this method
     class: double
     dimension: [1x1]
     default:   1000
categories: [ documentation , MDL01 , ControlParameterDependent]
class: ControlParameterDependent
layout: method
---
