---
title: ConjugateGradientDescent
data: 
   description: This method is used within the GradientMethod method. GradientMethod executes iteratively this rutine in order to get 
                one update of the control in each iteration. In the case of choosing ConjugateGradientDescent this function updates the
                control of the following way
                  $$u_{old}=u_{new}-\alpha_k s_k$$
                  where $s_k$ is the descent direction.
                  The optimal control problem is defined by
                  $$\min J=\min (\Psi (t,Y(T))+\int^T_0 L(t,Y,U)dt)$$
                  subject to
                  $$\frac{d}{dt}Y=f(t,Y,U).$$
                  The gradient of $J$ is
                  $$dJ=\partial_u H=\partial_uL+p\partial_uf$$
                  An $p$ is computed using
                  $$-\frac{d}{dt}p = f_Y (t,Y,U)p+L_Y(Y,U)$$
                  $$ p(T)=\psi_Y(Y(T))$$
                  Since one the expression of the gradient, we can start with an initial control, solve the adjoint problem and evaluate 
                  the gradient. Then one updates the initial control in the direction of the approximate gradient with a step size
                  $\alpha_k$. $\alpha_k$ is determined by trying to solve numerically the following
                  $$\min_{\alpha_k}J(y_k,u_k-\alpha_k s_k)$$
                  where $s_k$ is choosen using the gradient of $J$.
                  Then, the follow $s_{k+1}$ is compute by
                  $$ s_{k+1} = -dJ_{k+1} + \beta_{k} s_{k}$$
                  where
                  $$ \beta_{k} = || dJ_{k+1} || / || dJ_{k} ||$$
                  This routine will tell to GradientMethod to stop when the minimum tolerance of the derivative
                 (or the relative error, user's choice) is reached. Moreover there is a maximum of iterations allowed.
   little_description: This method is used within the GradientMethod method. GradientMethod executes iteratively this rutine in order to get 
                one update of the control in each iteration.
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
