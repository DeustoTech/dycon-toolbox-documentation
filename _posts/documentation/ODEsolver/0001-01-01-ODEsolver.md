---
data:
  description: This is a odesolver using mid-point rule for
                $$M(d^2u/dt^2)=Ku+f$$
  tutorial: P0013_Numerical_homogenizaton_for_wave_equation
  author: XinliangL
  MandatoryInputs:   
   M0: 
     description: massive matrix 
     class: double
     dimension: [nxn]
   K0:
     description: stiffness matrix  
     class: double
     dimension: [nxn]
   ui:
     description: initial value of u
     class: double
     dimension: [nx1]
   uti:
     description: initial value of ut
     class: double
     dimension: [nx1]
   f:
     description: source term
     class: double
     dimension: [nx1]
   T:
     description: time interval
     class: double
     dimension: [1x1]
   J:
     description: number of time step
     class: double
     dimension: [1x1]
  Outputs:
   u:
     description: solution
     class: double
     dimension: [nx1]
   ut:
     description: derivative of solution u
     class: double
     dimension: [nx1]

title: ODEsolver
categories: [documentation, MDL00]
layout: function

---
