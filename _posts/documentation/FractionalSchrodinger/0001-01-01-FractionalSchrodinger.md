---
data:
  author: UmbertoB
  date: 2017-04-01
  description: Solver the fractional Schrodinger equation in 1d 
  MandatoryInputs:  
    s:
        class:        double
        dimension:   1
        description: Order of the fractional Laplacian $(-dx^2)^s$
        WARNING:     s HAS TO BE CHOSEN IN THE INTERVAL (0,1) 
    L:
        class:         double
        dimension:    1
        description:  Define the interval of x, So x \in (-L,L)  
    N:
        class:        integer
        dimension:   1
        description: number of points in the space discretization 
    T:
        class:        double
        dimension:   1
        description: length of the time interval
    u0:
        class:        function handle
        dimension:   1
        description: initial datum u0(x)
  OptionalInputs:
    x:
        class:        double
        dimension:   1x(N+2)
        description: space partition
    t:
        class:        double
        dimension:   1xNt (Nt defined applying the CFL condition)
        description: time partition
    u:
        class:        double
        dimension:   NxNt
        description: solution of the equation

title: FractionalSchrodinger
categories: [documentation, MDL02]
layout: function
helpfile: /Users/jesusoroya/Documents/GitHub/DyCon-Computational-Platform/helps/MDL02_FiniteElement/functions
---

Gas a

## sasd

