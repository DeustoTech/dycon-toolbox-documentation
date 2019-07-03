---
layout: default
title: Dircet Methods
nav_order: 3
parent: Pontryagin Problems 
---

Instead of the Gradient method in the DyCon Toolbox, we may use Matlab built-in functions such as 'fmincon' or 'fminunc' for the optimizations. In this tutorial, we test 'fmincon' and 'GradientMethod' with the example 'Problem 6.3' in the following paper:


[1] : E. R. Edge and W. F. Powers. "Function-space quasi-Newton algorithms for optimal control problems with bounded controls and singular arcs." Journal of Optimization Theory and Applications 20.4 (1976): 455-479.

```matlab
clear

syms x1 x2 x3 x4 u1 t

Y = [x1; x2; x3; x4];
U = [u1];

A = [-0.5,      5,    0,    0;
       -5,   -0.5,    0,    0;
        0,      0, -0.6,   10;
        0,      0,  -10, -0.6];

B = [0; 1; 0; 1];

dynamics = A*Y + B*U;
dynamics = matlabFunction(dynamics,'Vars',{t,Y,U,sym.empty});
Nt = 100;
T = 4.2;
Y0 = [10; 10; 10; 10];
```


We choose solver 'ode23tb' to cover the stiff nature of the equations.

```matlab
iode = ode(dynamics,Y,U);
iode.InitialCondition = Y0;
iode.Solver = @ode23;
iode.FinalTime = T;
iode.Nt = Nt;

Psi = @(t,Y) (Y'*Y);
L   = @(t,Y,U) 0;

iCP = Pontryagin(iode,Psi,L);
```


After we defined 'Pontryagin' class, we may use the function 'Control2Functional' to indicate the cost as a function of the control. In this way, we may impliment 'fmincon'. The maximum and minimum of the control are given by -1 and 1.

```matlab
U0 = iode.Control.Numeric;
Umax = 1*ones(size(iode.Control.Numeric));
Umin = -1*ones(size(iode.Control.Numeric));
options = optimoptions(@fmincon,'display','iter','SpecifyObjectiveGradient',true);
[U1_tspan,J1_optimal] = fmincon(@(U)Control2Functional(iCP,U),U0,[],[],[],[],Umin,Umax,[],options);
%%[U1_tspan,J1_optimal] = fminunc(@(U)Control2Functional(iCP,U),U0,options);
```


```
                                            First-order      Norm of
 Iter F-count            f(x)  Feasibility   optimality         step
    0       1    4.226202e+00    0.000e+00    1.152e-01
    1       2    3.923764e+00    0.000e+00    1.091e-01    5.019e-01
    2       3    2.577178e+00    0.000e+00    7.862e-02    2.524e+00
    3       4    2.257460e+00    0.000e+00    6.667e-02    6.987e-01
    4       5    2.025004e+00    0.000e+00    7.305e-02    6.217e-01
    5       6    1.854776e+00    0.000e+00    7.797e-02    5.797e-01
    6       7    1.728235e+00    0.000e+00    8.178e-02    5.349e-01
    7       8    1.606103e+00    0.000e+00    8.566e-02    5.413e-01
    8       9    1.551198e+00    0.000e+00    8.747e-02    2.647e-01
    9      10    1.467688e+00    0.000e+00    9.028e-02    5.065e-01
   10      11    1.415788e+00    0.000e+00    9.211e-02    3.775e-01
   11      12    1.366385e+00    0.000e+00    9.393e-02    3.665e-01
   12      13    1.307117e+00    0.000e+00    9.619e-02    4.706e-01
   13      14    1.264573e+00    0.000e+00    9.793e-02    4.183e-01
   14      15    1.233036e+00    0.000e+00    6.167e-02    4.142e-01
   15      16    1.205619e+00    0.000e+00    4.012e-02    3.222e-01
   16      17    1.180792e+00    0.000e+00    4.043e-02    3.275e-01
   17      18    1.163971e+00    0.000e+00    4.046e-02    2.901e-01
   18      19    1.151355e+00    0.000e+00    4.062e-02    2.115e-01
   19      20    1.132852e+00    0.000e+00    3.187e-02    3.602e-01
   20      21    1.126697e+00    0.000e+00    2.871e-02    1.708e-01
   21      22    1.112628e+00    0.000e+00    2.793e-02    3.689e-01
   22      23    1.099486e+00    0.000e+00    2.766e-02    3.610e-01
   23      24    1.098810e+00    0.000e+00    1.570e-02    7.308e-02
   24      25    1.095231e+00    0.000e+00    9.232e-03    1.573e-01
   25      26    1.091548e+00    0.000e+00    7.579e-03    1.690e-01
   26      27    1.089355e+00    0.000e+00    6.429e-03    1.494e-01
   27      28    1.087930e+00    0.000e+00    6.434e-03    1.225e-01
   28      29    1.085041e+00    0.000e+00    6.431e-03    1.596e-01
   29      30    1.081792e+00    0.000e+00    6.425e-03    1.769e-01
   30      31    1.080402e+00    0.000e+00    5.279e-03    1.140e-01

                                            First-order      Norm of
 Iter F-count            f(x)  Feasibility   optimality         step
   31      32    1.078796e+00    0.000e+00    5.278e-03    1.026e-01
   32      33    1.077619e+00    0.000e+00    5.283e-03    9.718e-02
   33      34    1.076969e+00    0.000e+00    3.744e-03    8.794e-02
   34      35    1.076075e+00    0.000e+00    3.052e-03    8.412e-02
   35      36    1.075294e+00    0.000e+00    2.966e-03    6.984e-02
   36      38    1.075067e+00    0.000e+00    2.794e-03    2.911e-02
   37      40    1.074863e+00    0.000e+00    2.440e-03    3.835e-02
   38      53    1.074851e+00    0.000e+00    1.053e-03    7.734e-04
   39      54    1.020800e+00    0.000e+00    2.464e-03    6.191e-01
   40      55    1.011180e+00    0.000e+00    2.920e-03    1.146e-01
   41      56    1.006900e+00    0.000e+00    3.204e-03    2.396e-01
   42      57    1.005615e+00    0.000e+00    3.317e-03    1.395e-01
   43      58    1.005155e+00    0.000e+00    3.445e-03    2.101e-01
   44      59    1.004241e+00    0.000e+00    3.541e-03    1.282e-01
   45      60    1.004087e+00    0.000e+00    1.643e-03    2.665e-02
   46      62    1.004015e+00    0.000e+00    1.630e-03    1.160e-02
   47      63    1.003804e+00    0.000e+00    1.613e-03    2.960e-02
   48      64    1.003466e+00    0.000e+00    1.593e-03    2.356e-02

Local minimum possible. Constraints satisfied.

fmincon stopped because the size of the current step is less than
the default value of the step size tolerance and constraints are 
satisfied to within the default value of the constraint tolerance.


```


We can solve the same control problem using 'GradientMethod'.

```matlab
iCP.Constraints.MaxControl = 1;
iCP.Constraints.MinControl = -1;

U0 = zeros(iCP.Dynamics.Nt,iCP.Dynamics.ControlDimension);
GradientMethod(iCP,U0,'Graphs',false,'DescentAlgorithm',@AdaptativeDescent,'display','all')
U2_tspan = iCP.Solution.UOptimal;
J2_optimal = iCP.Solution.JOptimal;
```


```
    "error = 5.647307e+01 | Functional = 3.267927e+00 | norm(Gradient) = 1.295183e+01 | norm(U) = 1.662327e+00 | iter = 5"

    "error = 5.259393e+00 | Functional = 9.972504e-01 | norm(Gradient) = 7.210203e+00 | norm(U) = 9.473084e+00 | iter = 10"

    "error = 4.960797e+00 | Functional = 9.830185e-01 | norm(Gradient) = 7.170901e+00 | norm(U) = 9.963379e+00 | iter = 15"

    "error = 4.963533e+00 | Functional = 9.828142e-01 | norm(Gradient) = 7.172717e+00 | norm(U) = 9.961282e+00 | iter = 17"


    Solve with precision: 

        We obtain: J(u) = 9.828142E-01

        error = 4.963533E+00

    With 17 iterations,     In 7.3344 seconds


```

```matlab
plot(iode.tspan,[U1_tspan,U2_tspan])
xlabel('Time')
ylabel('Control')
legend(['Solution of fmincon, cost=',num2str(J1_optimal)],['Solution of GradientMethod, cost=',num2str(J2_optimal)])
```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/04-PontryaginProblems/T043/copiaRM_01.png)

