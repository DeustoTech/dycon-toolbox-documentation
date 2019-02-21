---
title: ClassicalDescent
data: 
   description: This method is used within the GradientMethod method. GradientMethod executes 
                iteratively the algorithms that we give it. In the case of choosing ClassicalDescent 
                this function updates the control of the following way 
                    $$ u_{old} = u_{new} + \alpha dJ $$
                where dJ has obtain with the optimality condition of
                pontryagin principle. The optimal control problem is define
                by
                $$ \min J = \min \Psi(t,Y(T)) + \int_0^T L(t,Y,U) dt $$
                subject to
                $$ Y = f(t,Y,U) $$ 
                following the Pontryagin principle 
                $$ dJ = \partial_u H = \partial_u L + p \partial_u f $$
                Since we have the expression of the gradient, we can start with an initial control,
                solve the adjoint problem and evaluate the gradient. Then we will update the initial 
                control with the gradient.
   little_description: This method is able to update the value of the control by decreasing the value of the functional. 
   autor: JOroya
   MandatoryInputs:   
     iCP: 
         description: Control Problem Object
         class: ControlProblem
         dimension: [1x1]
     tol: 
         description: Control Vector in time  
         class: double
         dimension: [M,iCP.tspan]
   OptionalInputs:
     LengthStep: 
         description: This paramter is the length step of the gradient
                        method. By default, this is 0.1
         class: double 
         dimension: [1x1]
   Outputs:
     Unew:
         description: Update of Control Vector  
         class: double
         dimension: [Mxlength(iCP.tspan)]
     Ynew:
         description: Update of State Vector 
         class: double
         dimension: [length(iCP.tspan)]
     Jnew:
         description: New Value of functional 
         class: double
         dimension: [1x1]
     dJnew:
         description: New Value of gradient 
         class: double
         dimension: [1x1]
     error:
         description: the error $\vert dJ \vert / \vert U \vert $  
         class: double
         dimension: [1x1]
     stop:
         description: New Value of functional 
         class: logical
         dimension: [1x1]
categories: [ documentation , MDL01 , OptimalControl]
class: OptimalControl
layout: method
---
