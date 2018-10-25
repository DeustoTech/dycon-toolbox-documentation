---
  layout: function
  categories: Functions
  title: rigidity_fr_laplacian
  author: UmbertoB
  date: 2017-04-01
  short_description: Stiffness matrix for the FE discretization of the
                     1d fractional Laplacian.
  long_description: Computes the rigidity matrix for the FE discretization 
                    of the fractional Laplacian (-dx^2)^s on the space 
                    domain (-L,L).
  inputs_variables:  
    s:
        type:        double
        dimension:   1
        description: Order of the fractional Laplacian (-dx^2)^s
        WARNING:     S HAS TO BE CHOSNE IN THE INTERVAL (0,1) 
    L:
        type:         double
        dimension:    1
        description:  Define the interval of x, So x \in (-L,L)  
    N:
        type:        integer
        dimension:   1
        description: number of points in the space discretization 
  outputs_variables:
    A:
        type:        double
        dimension:   NxN
        description: Rigidity Matrix of fractional Laplacian
---
<hr>
## Description


Summary of example objective



## Section 1 Title


Description of first code block



```matlab
a = 1;
```



## Section 2 Title


Description of second code block



```matlab
b = 2;
```



