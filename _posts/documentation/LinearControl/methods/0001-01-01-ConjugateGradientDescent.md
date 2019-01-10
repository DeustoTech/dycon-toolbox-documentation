---
title: ConjugateGradientDescent
data: 
   description: This method is able to update the value of the control by decreasing 
                the value of the functional. By calculating the gradient, $ \frac{dH}{du}$. Also, it is decremented 
                in that direction, assuring the decrease by the adaptive step size. 
   autor: UmbertoB
   MandatoryInputs:   
     iCP: 
         description: Control Problem Object
         class: ControlProblem
         dimension: [1x1]
     UOld: 
         description: Control Vector in time  
         class: double
         dimension: [M,iCP.tline]
     YOld: 
         description: State Vector in time 
         class: double
         dimension: [length(iCP.ode.Y0),iCP.tline]
     JOld: 
         description: Value of functional J(Uold,Yold)
         class: double
         dimension: [length(iCP.ode.Y0),iCP.tline]
   Outputs:
     Unew:
         description: Update of Control Vector  
         class: double
         dimension: [Mxlength(iCP.tline)]
     Ynew:
         description: Update of State Vector 
         class: double
         dimension: [length(iCP.tline)]
     Jnew:
         description: New Value of functional 
         class: double
         dimension: [1x1]
categories: [ documentation , MDL01 , LinearControl]
class: LinearControl
layout: method
---
