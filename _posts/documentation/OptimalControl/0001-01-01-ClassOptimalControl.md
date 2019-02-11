---
description: "This class is able to solve optimization problems of a function restricted to an ordinary equation.
              This scheme is used to solve optimal control problems in which the functional derivative is calculated. 
              <strong>OptimalControl</strong> class has methods that help us find optimal control as well as obtaining 
              the attached problem and it's derivative form, 
              in both Symbolic and numerical versions."
long: "This class is able to solve optimization problems of a function restricted to an ordinary equation.
              This scheme is used to solve optimal control problems in which the functional derivative is calculated. 
              <strong>OptimalControl</strong> class has methods that help us find optimal control as well as obtaining 
              the attached problem and it's derivative form, 
              in both Symbolic and numerical versions. Este problema se
              aborda con el metodo del gradiente. Dado que la informacion
              del problema esta en simbolico, podemos calcular el
              gradiente y el problema adjunto mediante el principio de
              pontryagin. Se ha implementado el metodo del gradiente,
              de forma que el calculo de descenso sea un parametro. Por
              defecto, este descenso se calcula con el metodo del
              gradiente conjugado.
              http://web.mit.edu/mitter/www/publications/2_conjugate_grad_IEEEAC.pdf"
title: OptimalControl
categories: [documentation, MDL01]
layout: class
type: constructor
properties:
   J: 
        type: "Functional"
        default: "none"
        description: "This property represent the cost of optimal control"
      
   ode: 
        type: ode
        default: none
        description: This property represented ordinary differential equation
      
   adjoint: 
        type: double
        default: function_handle
        description: The derivative of the Hamiltonian with respect to the control u 
      
   hamiltonian: 
        type: double
        default: function_handle
        description: The derivative of the Hamiltonian with respect to the control u 
      
   gradient: 
        type: struct
        default: none
        description: The adjoint propertir contain the numerical function that represents the adjoint problem this struct have a two properties. The first is dP_dt and the second is P0.   
      
   solution: 
        type: double
        default: none
        description: It is an array that contains the different functional values during the execution of the optimization algorithm that has been used.
      
   YT: 
methods:
   OptimalControl:
        name: ControlProblem
        description: 
        autor: JOroya
        MandatoryInputs:   
          iode: 
              name: Ordinary Differential Equation 
              description: Ordinary Differential Equation represent the constrain to minimization the functional 
              class: ode
              dimension: [1x1]
          Jfun: 
              name: functional
              description: Cost function to obtain the optimal control 
              class: Functional
              dimension: [1x1]        
        OptionalInputs:
          T:
              name: Final Time 
              description: This parameter represent the final time of simulation.  
              class: double
              dimension: [1x1]
              default: iode.T 
          dt:
              name: Final Time 
              description: This parameter represent is the interval to interpolate the control, $u$, and state, $y$, to obtain the functional $J$ and the gradient $dH/du$
              class: double
              dimension: [1x1]
              default: iode.dt         
        Outputs:
          obj:
              name: ControlProblem MATLAB
              description: ControlProblem MATLAB class
              class: ControlProblem
              dimension: [1x1]
        url: /documentation/mdl01/OptimalControl/OptimalControl
   AdaptativeDescent:
         description: This method is able to update the value of the control by decreasing 
                      the value of the functional. By calculating the gradient, $ \frac{dH}{du}$. Also, it is decremented 
                      in that direction, assuring the decrease by the adaptive step size. 
         little_description: This method is able to update the value of the control by decreasing the value of the functional. 
         autor: JOroya
         MandatoryInputs:   
           iCP: 
               description: Control Problem Object
               class: ControlProblem
               dimension: [1x1]
           UOld: 
               description: Control Vector in time  
               class: double
               dimension: [M,iCP.tspan]
           YOld: 
               description: State Vector in time 
               class: double
               dimension: [length(iCP.ode.Y0),iCP.tspan]
           JOld: 
               description: Value of functional J(Uold,Yold)
               class: double
               dimension: [length(iCP.ode.Y0),iCP.tspan]
         OptionalInputs:
           InitialLengthStep: 
               description: This parameter is the step size if the MiddleStepControl option is false. 
                              If the option MiddleStepControl is activated then this parameter is the initial step
                              of the methodo but then the step is doubled in the case where the functional iteration 
                              decreases and is divided by two its the functional one grows.
               class: double
               dimension: [1x1]
           MinLengthStep: 
               description: It may happen that although we divide the step of the descenco many times,
                              we continue to obtain an update that increases the value of the functional. In this case,
                              it is necessary to have a minimum step size to avoid infinite loops. This parameter is
                              responsible for this.
               class: double
               dimension: [1x1]
           MiddleStepControl: 
               description: If this parameter is enabled, it allows the algorithm to search for different 
                              step-logitudes, provided that the control update decrements the functional value. If it is
                              deactivated, the descent of the gradient will be constant.
               class: double
               dimension: [length(iCP.ode.Y0),iCP.tspan]
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
         url: /documentation/mdl01/OptimalControl/AdaptativeDescent
   ClassicalDescent:
         description: This method is able to update the value of the control by decreasing 
                      the value of the functional. By calculating the gradient, $ \frac{dH}{du}$. Also, it is decremented 
                      in that direction, assuring the decrease by the adaptive step size. 
         little_description: This method is able to update the value of the control by decreasing the value of the functional. 
         autor: JOroya
         MandatoryInputs:   
           iCP: 
               description: Control Problem Object
               class: ControlProblem
               dimension: [1x1]
           UOld: 
               description: Control Vector in time  
               class: double
               dimension: [M,iCP.tspan]
           YOld: 
               description: State Vector in time 
               class: double
               dimension: [length(iCP.ode.Y0),iCP.tspan]
           JOld: 
               description: Value of functional J(Uold,Yold)
               class: double
               dimension: [length(iCP.ode.Y0),iCP.tspan]
         OptionalInputs:
           InitialLengthStep: 
               description: This parameter is the step size if the MiddleStepControl option is false. 
                              If the option MiddleStepControl is activated then this parameter is the initial step
                              of the methodo but then the step is doubled in the case where the functional iteration 
                              decreases and is divided by two its the functional one grows.
               class: double
               dimension: [1x1]
           MinLengthStep: 
               description: It may happen that although we divide the step of the descenco many times,
                              we continue to obtain an update that increases the value of the functional. In this case,
                              it is necessary to have a minimum step size to avoid infinite loops. This parameter is
                              responsible for this.
               class: double
               dimension: [1x1]
           MiddleStepControl: 
               description: If this parameter is enabled, it allows the algorithm to search for different 
                              step-logitudes, provided that the control update decrements the functional value. If it is
                              deactivated, the descent of the gradient will be constant.
               class: double
               dimension: [length(iCP.ode.Y0),iCP.tspan]
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
         url: /documentation/mdl01/OptimalControl/ClassicalDescent
   ConjugateGradientDescent:
         description: This method is able to update the value of the control by decreasing 
                      the value of the functional. By calculating the gradient, $ \frac{dH}{du}$. Also, it is decremented 
                      in that direction, assuring the decrease by the adaptive step size. 
         little_description: This method is able to update the value of the control by decreasing the value of the functional. 
         autor: JOroya
         MandatoryInputs:   
           iCP: 
               description: Control Problem Object
               class: ControlProblem
               dimension: [1x1]
           UOld: 
               description: Control Vector in time  
               class: double
               dimension: [M,iCP.tspan]
           YOld: 
               description: State Vector in time 
               class: double
               dimension: [length(iCP.ode.Y0),iCP.tspan]
           JOld: 
               description: Value of functional J(Uold,Yold)
               class: double
               dimension: [length(iCP.ode.Y0),iCP.tspan]
         OptionalInputs:
           InitialLengthStep: 
               description: This parameter is the step size if the MiddleStepControl option is false. 
                              If the option MiddleStepControl is activated then this parameter is the initial step
                              of the methodo but then the step is doubled in the case where the functional iteration 
                              decreases and is divided by two its the functional one grows.
               class: double
               dimension: [1x1]
           MinLengthStep: 
               description: It may happen that although we divide the step of the descenco many times,
                              we continue to obtain an update that increases the value of the functional. In this case,
                              it is necessary to have a minimum step size to avoid infinite loops. This parameter is
                              responsible for this.
               class: double
               dimension: [1x1]
           MiddleStepControl: 
               description: If this parameter is enabled, it allows the algorithm to search for different 
                              step-logitudes, provided that the control update decrements the functional value. If it is
                              deactivated, the descent of the gradient will be constant.
               class: double
               dimension: [length(iCP.ode.Y0),iCP.tspan]
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
         url: /documentation/mdl01/OptimalControl/ConjugateGradientDescent
   Copy:
        description: This method adds the problem adjoint to the Control Problem object, since we have
                      $$ \dot{\textbf{Y}} = f(\textbf{Y},t) $$ 
                      and the functional
                      $$ J = \Psi(\textbf{Y}(T)) + \int_{0}^T L(\textbf{Y},U,t)dt $$ 
                      we can create the Hamiltonian 
                      $$ H = L + P*F $$
                      where $\textbf{P} = [p_1 p_2 p_3 ... ]^T$ . So according to the principle of the maximum of pontriagin,
                      we can calculate the attached problems through the formulas
                      $$ \frac{d\textbf{P}}{dt} = \vec{\nabla}_{Y} H = 
                      (\frac{\partial H}{ \partial y_1},\frac{\partial H}{ \partial y_2},...)$$
                      with the final time condition
                      $$ \textbf{P}(T) = 
                      (\frac{\partial \Psi}{ \partial y_1},\frac{\partial \Psi}{ \partial y_2},...)$$
        little_description: Method capable of obtaining the attached problem and its final condition.
        autor: JOroya
        MandatoryInputs:   
           iCP: 
               name: Control Problem
               description: Control problem object
               class: ControlProblem
               dimension: [1x1]
        url: /documentation/mdl01/OptimalControl/Copy
   GetAdjointProblem:
        description: This method adds the problem adjoint to the Control Problem object, since we have
                      $$ \dot{\textbf{Y}} = f(\textbf{Y},t) $$ 
                      and the functional
                      $$ J = \Psi(\textbf{Y}(T)) + \int_{0}^T L(\textbf{Y},U,t)dt $$ 
                      we can create the Hamiltonian 
                      $$ H = L + P*F $$
                      where $\textbf{P} = [p_1 p_2 p_3 ... ]^T$ . So according to the principle of the maximum of pontriagin,
                      we can calculate the attached problems through the formulas
                      $$ \frac{d\textbf{P}}{dt} = \vec{\nabla}_{Y} H = 
                      (\frac{\partial H}{ \partial y_1},\frac{\partial H}{ \partial y_2},...)$$
                      with the final time condition
                      $$ \textbf{P}(T) = 
                      (\frac{\partial \Psi}{ \partial y_1},\frac{\partial \Psi}{ \partial y_2},...)$$
        little_description: Method capable of obtaining the attached problem and its final condition.
        autor: JOroya
        MandatoryInputs:   
           iCP: 
               name: Control Problem
               description: Control problem object
               class: ControlProblem
               dimension: [1x1]
        url: /documentation/mdl01/OptimalControl/GetAdjointProblem
   GetFunctional:
        description: Method capable of calculating the value of the functional defined in the control problem.
        little_description: Method capable of calculating the value of the functional defined in the control problem.
        autor: JOroya
        MandatoryInputs:   
         iCP: 
           description:  Control Problem
           class: ControlProblem
           dimension: [1x1]
         Y: 
           name: Solution of ODE
           description: 
           class: ControlProblem
           dimension: [1x1]
         U: 
           name: matrix of control
           description: 
           class: ControlProblem
           dimension: [1x1]
        Outputs:
         JValue:
           name: Functional value with this U and Y 
           description: double 
           class: double
           dimension: [1x1]
        url: /documentation/mdl01/OptimalControl/GetFunctional
   GetGradient:
        description: Creates the iCP.dH_du property that contains a numeric function that 
                      returns the value of the gradient given the dynamics solution, 
                      $Y$ and the associated control, $U$.
        little_description: Creates the iCP.dH_du property that contains a numeric function that 
                      returns the value of the gradient given the dynamics solution, 
                      $Y$ and the associated control, $U$. 
        autor: JOroya
        MandatoryInputs:   
         iCP: 
           name: Control Problem
           description: 
           class: ControlProblem
           dimension: [1x1]
        url: /documentation/mdl01/OptimalControl/GetGradient
   GetNumericalGradient:
         description: This method is able to update the value of the control by decreasing 
                      the value of the functional. By calculating the gradient, $ \frac{dH}{du}$. Also, it is decremented 
                      in that direction, assuring the decrease by the adaptive step size. 
         little_description: This method is able to update the value of the control by decreasing the value of the functional. 
         autor: JOroya
         MandatoryInputs:   
           iCP: 
               description: Control Problem Object
               class: ControlProblem
               dimension: [1x1]
           UOld: 
               description: Control Vector in time  
               class: double
               dimension: [M,iCP.tspan]
           YOld: 
               description: State Vector in time 
               class: double
               dimension: [length(iCP.ode.Y0),iCP.tspan]
           JOld: 
               description: Value of functional J(Uold,Yold)
               class: double
               dimension: [length(iCP.ode.Y0),iCP.tspan]
         OptionalInputs:
           InitialLengthStep: 
               description: This parameter is the step size if the MiddleStepControl option is false. 
                              If the option MiddleStepControl is activated then this parameter is the initial step
                              of the methodo but then the step is doubled in the case where the functional iteration 
                              decreases and is divided by two its the functional one grows.
               class: double
               dimension: [1x1]
           MinLengthStep: 
               description: It may happen that although we divide the step of the descenco many times,
                              we continue to obtain an update that increases the value of the functional. In this case,
                              it is necessary to have a minimum step size to avoid infinite loops. This parameter is
                              responsible for this.
               class: double
               dimension: [1x1]
           MiddleStepControl: 
               description: If this parameter is enabled, it allows the algorithm to search for different 
                              step-logitudes, provided that the control update decrements the functional value. If it is
                              deactivated, the descent of the gradient will be constant.
               class: double
               dimension: [length(iCP.ode.Y0),iCP.tspan]
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
         url: /documentation/mdl01/OptimalControl/GetNumericalGradient
   GradientMethod:
        name: GradientMethod
        little_description: The gradient method is able to optimize the given functional, going down the gradient.
        description: "The gradient method is able to optimize the given
                              functional, going down the gradient. El calculo del gradiente puede
                              ser de varios tipo. Por defecto la direccion y el modulo de descenso
                              se calcula con el gradiente conjugado
                              http://web.mit.edu/mitter/www/publications/2_conjugate_grad_IEEEAC.pdf"
        autor: JOroya
        MandatoryInputs:   
          iCP: 
              name: Control Problem
              description: 
              class: ControlProblem
              dimension: [1x1]
        OptionalInputs:
          U0:
              name: Initial Control 
              description: matrix 
              class: double
              dimension: [length(iCP.tspan)]
              default: zeros
          MaxIter:
              name: Initial Control 
              description: matrix 
              class: double
              dimension: [1x1]
              default: 50
          tol:
              name: Initial Control 
              description: matrix 
              class: double
              dimension: 
              dimension: [1x1]
          DescentParameters:
              description: Parmater of Descent Method 
              class: double
              dimension: cell
              default: cell.empty    
          Graphs:
              description: Parameter that indicate if the method must plot the optimization, while is calculate 
              class: logical
              dimension: [1x1]
              default: false        
          TypeGraphs:
              description: Type of graphs. This parameter can be 'ODE' or 'PDE' 
              class: string
              dimension: [1x1]
              default: 'ODE'
          SaveGif:
              name: If this parameter is true, A gif of the optimization process is created
              description: matrix 
              class: double
              dimension: [length(iCP.tspan)]
              default: false
          restart:
              description: The optimization start with U0 = iCP.UOptimal
              class: double
              dimension: [1x1]
              default: false
        url: /documentation/mdl01/OptimalControl/GradientMethod
   plot:
        name: GradientMethod
        description: Since most of the optimization methods require an iterative process, plot shows how the dynamics, 
                      the control and the functional in the optimization evolve.
        little_description: shows how the dynamics, the control and the functional in the optimization evolve.
        autor: JOroya
        MandatoryInputs:   
          iCP: 
              name: Control Problem
              description: 
              class: ControlProblem
              dimension: [1x1]
        OptionalInputs:
          Graphs:
              description: Parameter that indicate if the method must plot the optimization, while is calculate 
              class: logical
              dimension: [1x1]
              default: false        
          TypeGraphs:
              description: Type of graphs. This parameter can be 'ODE' or 'PDE' 
              class: string
              dimension: [1x1]
              default: 'ODE'
          SaveGif:
              name: If this parameter is true, A gif of the optimization process is created
              description: matrix 
              class: double
              dimension: [length(iCP.tspan)]
              default: false
        url: /documentation/mdl01/OptimalControl/plot
   resume:
        description: show the most importants parameters of the control problem
        little_description: show the most importants parameters of the control problem
        autor: JOroya
        MandatoryInputs:   
           iCP: 
               description: Control Problem Object
               type: ControlProblem
        url: /documentation/mdl01/OptimalControl/resume

---

First define the vectors


$$ symY = \left( \begin{matrix}   y1 \\                                   y2                  \end{matrix} \right)    symU = \left( \begin{matrix}   u1 \\                                   u2                   \end{matrix} \right) $$

```matlab
clear;
syms t
symY = sym('y',[2 1]);
symU = sym('u',[1 1]);
```


**Ordinary differential equation**


In this case we will define the following differential equation


$$ \left( \begin{matrix}   \dot{S} \\                            \dot{I}                  \end{matrix} \right)    =       \left( \begin{matrix}   \lambda - \beta S I - \sigma_1 S \\                               \beta S I - u_1 I - \sigma_2 I                   \end{matrix} \right) $$

```matlab
Lambda = 1;beta = 0.5;
sigma1 = 0.1;sigma2 = 0.1;

S = symY(1);I = symY(2);
Fsym(1)  = Lambda - beta*S*I -  sigma1*S;
Fsym(2)  = beta*S*I - symU(1)*I - sigma2*I ;
```

```matlab
FinalTime = 5;
S0 = 100 ;I0 = 15;
Y0 = [ S0 ; I0];
Dynamics = ode(Fsym.',symY,symU,'Condition',Y0,'FinalTime',FinalTime);
```


**Cost Functional**


$$ J = \Psi(Y(T),t) + \int_0^T L(Y(t,U),U(t),t) dt$$


In this case,


$$ J = A \int_0^T (\vert U \vert^2 + I) dt$$


Now, We can create the control problem

```matlab
A = 1;
symPsi  = sym(0);
symL    = A*(symU.'*symU) + I;
%
iCP1 = OptimalControl(Dynamics,symPsi,symL);
```


and solve by Classical Gradient Method

```matlab
GradientMethod(iCP1)
```


```

    Solve with presicion: 

        We obtain: J(u) = 4.414871E+01

        mean(||dJ_i||) = 4.801581E-02

    With 7 iterations,     In 6.9807 seconds


```

```matlab
plot(iCP1)
```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/MDL01/class/main/OptimalControl/copiaRM_01.png)

