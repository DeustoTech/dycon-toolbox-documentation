---
data:
  author: Domenec
  date: 2018-12-19
  description: This function computes an approximate null-control for the semilinear heat equation. Consider the semilinear 
                heat equation in the interval $[0,1]$ with interior control, $$y_t-Dy_{xx}=G(y)+u\mathbb{1}_\omega$$ with 
                0 Dirichlet boundary conditions. The control is computed via an optimal control problem. WARNING the control
                might be non optimum with respect to the functional. It will depend on the non-linearity considered in the heat 
                equation, the convexity of the functional has to be proven. Given the time horizon for the control $T>0$, the
                functional considered is $$J(y,u)=\|y(T)\|_{L^2(\Omega)}+\beta\int_0^T \|u(t)\|^2_{L^2(\Omega)}dt.$$ Computations
                are done with the DyCon toolbox considering a semi-discretization on space and integrating the ODE system.
  MandatoryInputs:  
    N:
        class:        integer
        dimension:   1
        description: Number of interior points in the semi-discretization
    D:
        class:         double
        dimension:    1
        description:  Diffusivity constant  
    G:
        class:        symbolic expression
        dimension:   1
        description: Symbolic expression of the non-linearity
    T:
        class:        double
        dimension:   1
        description: Time horizon
    beta:
        class:        double
        dimension:   1
        description: parameter in the functional $J$
    w:
        class:        double
        dimension:   2
        description: vector containing the borders of the interior control region
    beta:
        class:        handle function
        dimension:   1
        description: handle function containing the initial data $y_0$
  Outputs:
    freedynamics:
        class:        structure
        dimension:   1x1
        description: the structure contains the necessary data for plotting the free dynamics i.e. the dynamics without control.
                        <ul>
                            <li>freedynamics.time is the time mesh</li>
                            <li>freedynamics.space is the space mesh</li>
                            <li>freedynamics.value is the values of the solution in the mesh</li>
                        </ul>
    controlleddynamics:
        class:        structure
        dimension:   1x1
        description: the structure contains the necessary data for plotting the controlled dynamics i.e. the dynamics with the control computed via gradient descent over the functional.
                        <ul>
                            <li>controlleddynamics.time is the time mesh</li>
                            <li>controlleddynamics.space is the space mesh</li>
                            <li>controlleddynamics.value is the values of the solution in the mesh</li>
                        </ul>
    ucontrol:
        class:        structure
        dimension:   1x1
        description: the structure contains the necessary data for plotting the computed control in the control region.
                        <ul>
                            <li>ucontrol.time is the time mesh</li>
                            <li>ucontrol.space is the space mesh</li>
                            <li>ucontrol.value is the values of the control in the mesh corresponding to the control region</li>
                        </ul>
    targetplusdynamicspluscontrol:
        class:        structure
        dimension:   1x1
        description: the structure contains the necessary data for plotting the free dynamics at time $T$ the control dynamics at time $T$ and the desired target (the function 0).
                        <ul>
                             <li>targetplusdynamicspluscontrol.y1 is the target </li>
                             <li>targetplusdynamicspluscontrol.y2 is the free dynamics at time $T$</li>
                             <li>targetplusdynamicspluscontrol.y3 is the dynamics with control at time $T$. </li>
                        </ul>

title: SLSD1doptimalnullcontrol
categories: [documentation, MDL01]
layout: function
---
