---
description: "This class is able to solve optimization problems of a function restricted to an ordinary equation.
              This scheme is used to solve optimal control problems in which the functional derivative is calculated. 
              <strong>OptimalControl</strong> class has methods that help us find optimal control as well as obtaining 
              the attached problem and it's derivative form, 
              in both Symbolic and numerical versions."
long:  This class is able to solve optimal control problems. Optimal control refers to the problem of finding a control law
          for a given system such that a certain optimality criterion is achieved. The essential features of an optimal control problem are 
              <ul>
              <li> a cost functional to be minimized;</li>
              <li> an initial/boundary value problem for a differential equation describing the motion, in order to determine the state of the system;</li>
              <li> a control function;</li>
              <li> eventual constraints that have to be obeyed.</li>
              </ul>
              The control may be freely chosen within the given constraints, while the state is uniquely determined by the differential equation and the initial conditions.
              We have to choose the control in such a way that the cost function is minimized. This class allows treating general optimal control problems in the form
              $$ \begin{equation*}
                  \min_{u\in\mathcal{U}} J,
              \end{equation*} $$
               in which the objective functional $J$ is defined as
               $$ \begin{equation*}
                  J=\Psi (x(T))+\int _{0}^{T}\mathcal{L}(x(t),u(t)),dt
              \end{equation*} $$
              and where $x$ is the state of a dynamical system with input $u\in\mathcal{U}$, the set of admissible controls 
              $$\begin{equation*} \dot {x}=f(x,u),\quad x(0)=x_{0},\quad
              u(t)\in\mathcal {U},\quad t\in [0,T]. \end{equation*}$$
              Moreover, the class permits to choose among different methods for solving the minimization problem. At the present stage, the methods available are
                <ul>
                  <li>  <a href='https://deustotech.github.io/dycon-platform-documentation/documentation/mdl01/optimalcontrol/ClassicalDescent'>Classical gradient method</a></li>
                  <li>  <a href='https://deustotech.github.io/dycon-platform-documentation/documentation/mdl01/optimalcontrol/AdaptativeDescent'>Gradient method with adaptive descend step</a></li>
                  <li>  <a href='https://deustotech.github.io/dycon-platform-documentation/documentation/mdl01/optimalcontrol/ConjugateGradientDescent'>Conjugate gradient method</a></li>
                </ul>
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
         description: This method is used within the GradientMethod method. GradientMethod executes iteratively this rutine
                      in order to get one update of the control in each iteration. In the case of choosing AdaptativeDescent 
                      this function updates the control of the following way
                        $$u_{old}=u_{new}-\alpha_k dJ$$
                        where dJ is an approximation of the gradient of J that has been obtained considering the adjoint state of the optimality condition of Pontryagin principle. The optimal control problem is defined by
                        $$\min J=\min\Psi (t,Y(T))+\int^T_0 L(t,Y,U)dt$$
                        subject to
                        $$\frac{d}{dt}Y=f(t,Y,U).$$
                        The gradient of $$J$$ is
                        $$dJ=\partial_u H=\partial_uL+p\partial_uf$$
                        An approximation $$p$$ is computed using
                        $$-\frac{d}{dt}p = f_Y (t,Y,U)p+L_Y(Y,U)$$
                        $$ p(T)=\psi_Y(Y(T))$$
                        Since one the expression of the gradient, we can start with an initial control, solve the adjoint problem and evaluate the gradient. Then one updates the initial control in the direction of the approximate gradient with a step size $$\alpha_k$$. $$\alpha_k$$ is determined by a small variation of the Armijo stepsize rule. In each iteration the algorithm multiplies the stepsize by to $$\alpha_k=2\alpha_{k-1}$$ and checks if $$J(y_k,u_k)<J(y_{k-1},u_{k-1})$$ in case to be true continues to the next iteration, in case to be false it devides by two the stepsize until the condition is fulfilled or the minimum stepsize is reached.
                        In this routine the user has to choose the minimum step size.
                        This routine will tell to GradientMethod to stop when the minimum tolerance of the derivative (or the relative error, user's choice) is reached. Moreover there is a maximum of iterations allowed.
         little_description: This method is used within the GradientMethod method. GradientMethod executes iteratively this rutine
                      in order to get one update of the control in each iteration.
         autor: JOroya
         MandatoryInputs:   
           iCP: 
               description: Control problem object, it carries all the information about the dynamics, the functional to be minimized and moreover the updates of the current best control find so far.
               class: ControlProblem
               dimension: [1x1]
           tol: 
               description: the tolerance desired.  
               class: double
               dimension: [1x1]
         OptionalInputs:
           InitialLengthStep: 
               description: This parameter is the length step of the gradient method that is going to be used at the begining of the process. By default, this is 0.1.
               class: double
               dimension: [1x1]
           MinLengthStep: 
               description: This paramter is the lower bound on the length step of the gradient method if the algorithm needs to have a step size lower than this size it will make the GradientMethod stop.
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
         url: /documentation/mdl01/OptimalControl/AdaptativeDescent
   ClassicalDescent:
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
         url: /documentation/mdl01/OptimalControl/ClassicalDescent
   CoConjugateGradientDescent:
         description: This method is used within the GradientMethod method. GradientMethod executes 
                      iteratively the algorithms that we give it. In the case of choosing ClassicalDescent 
                      this function updates the control of the following way 
                          $$ u_{old} = u_{new} + \\alpha dJ $$
                      where dJ has obtain with the optimality condition of
                      pontryagin principle. The optimal control problem is define
                      by
                      $$ \\min J = \\min \\Psi(t,Y(T)) + \\int_0^T L(t,Y,U) dt $$
                      subject to
                      $$ Y = f(t,Y,U) $$ 
                      following the Pontryagin principle 
                      $$ dJ = \\partial_u H = \\partial_u L + p \\partial_u f $$
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
               description: the error $\\vert dJ \\vert / \\vert U \\vert $  
               class: double
               dimension: [1x1]
           stop:
               description: New Value of functional 
               class: logical
               dimension: [1x1]
         url: /documentation/mdl01/OptimalControl/CoConjugateGradientDescent
   CoGradientMethod:
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
        url: /documentation/mdl01/OptimalControl/CoGradientMethod
   ConjugateGradientDescent:
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
         url: /documentation/mdl01/OptimalControl/ConjugateGradientDescent
   Copy:
        description: This method adds the problem adjoint to the Control Problem object, since we have
                      $$ \\dot{\\textbf{Y}} = f(\\textbf{Y},t) $$ 
                      and the functional
                      $$ J = \\Psi(\\textbf{Y}(T)) + \\int_{0}^T L(\\textbf{Y},U,t)dt $$ 
                      we can create the Hamiltonian 
                      $$ H = L + P*F $$
                      where $\\textbf{P} = [p_1 p_2 p_3 ... ]^T$ . So according to the principle of the maximum of pontriagin,
                      we can calculate the attached problems through the formulas
                      $$ \\frac{d\\textbf{P}}{dt} = \\vec{\\nabla}_{Y} H = 
                      (\\frac{\\partial H}{ \\partial y_1},\\frac{\\partial H}{ \\partial y_2},...)$$
                      with the final time condition
                      $$ \\textbf{P}(T) = 
                      (\\frac{\\partial \\Psi}{ \\partial y_1},\\frac{\\partial \\Psi}{ \\partial y_2},...)$$
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
                      $$ \\dot{\\textbf{Y}} = f(\\textbf{Y},t) $$ 
                      and the functional
                      $$ J = \\Psi(\\textbf{Y}(T)) + \\int_{0}^T L(\\textbf{Y},U,t)dt $$ 
                      we can create the Hamiltonian 
                      $$ H = L + P*F $$
                      where $\\textbf{P} = [p_1 p_2 p_3 ... ]^T$ . So according to the principle of the maximum of pontriagin,
                      we can calculate the attached problems through the formulas
                      $$ \\frac{d\\textbf{P}}{dt} = \\vec{\\nabla}_{Y} H = 
                      (\\frac{\\partial H}{ \\partial y_1},\\frac{\\partial H}{ \\partial y_2},...)$$
                      with the final time condition
                      $$ \\textbf{P}(T) = 
                      (\\frac{\\partial \\Psi}{ \\partial y_1},\\frac{\\partial \\Psi}{ \\partial y_2},...)$$
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
                      the value of the functional. By calculating the gradient, $ \\frac{dH}{du}$. Also, it is decremented 
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


and solve by Classical Gradient Methodcla

```matlab
GradientMethod(iCP1,'DescentAlgorithm',@ClassicalDescent)
```


```
error = 0
error = 5
error = 3.3322
error = 3.3303
error = 3.3249
error = 3.3057
error = 3.2306
error = 2.9476
error = 2.0529
error = 0.51149
error = 0.062916
error = 0.0024618

    Solve with presicion: 

        We obtain: J(u) = 4.419742E+01

        mean(||dJ_i||) = 2.461753E-03

    With 12 iterations,     In 1.0835 seconds


```

```matlab
plot(iCP1)
```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/MDL01/class/main/OptimalControl/copiaRM_01.png)

