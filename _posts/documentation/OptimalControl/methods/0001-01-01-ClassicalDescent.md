---
title: ClassicalDescent
data: 
   description: This method is used within the GradientMethod method. GradientMethod executes iteratively this rutine in 
                  order to get one update of the control in each iteration. In the case of choosing ClassicalDescent this function 
                  updates the control of the following way
                  $$u_{old}=u_{new}-\alpha dJ$$
                  where dJ is an approximation of the gradient of J that has been obtained considering the adjoint state of the 
                  optimality condition of Pontryagin principle. The optimal control problem is defined by
                  $$\min J=\min\Psi (t,Y(T))+\int^T_0 L(t,Y,U)dt$$
                  subject to
                  $$\frac{d}{dt}Y=f(t,Y,U)$$
                  The gradient of $J$ is
                  $$dJ=\partial_u H=\partial_uL+p\partial_uf$$
                  An approximation $p$ is computed using
                  $$-\frac{d}{dt}p = f_Y (t,Y,U)p+L_Y(Y,U)$$
                  $$ p(T)=\psi_Y(Y(T))$$
                  Since one the expression of the gradient, we can start with an initial control, 
                  solve the adjoint problem and evaluate the gradient. Then we will update the initial control in 
                  the direction of the approximate gradient with a step size $\alpha$.
                  In this routine the user has to choose the step size.
                  WARNING Using this routine the GradientMethod might not converge if the stepsize is not choosen properly or
                  being slow if the step size is choosen very small. For an adaptative stepsize with Armijo Rule guaranteeing the
                  convergence see (adaptative stepsize).
                  This routine will tell to GradientMethod to stop when the minimum tolerance of the derivative 
                  (or the relative error, user's choice) is reached. Moreover there is a maximum of iterations allowed.
   little_description: GradientMethod executes iteratively this rutine in 
                        order to get one update of the control in each iteration. 
                        In the case of choosing ClassicalDescent this function 
                updates the control
   autor: [DomenecR,JOroya]
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
         description: This parameter is the length step of the gradient method that is going to be used. By default, this is 0.1.
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
