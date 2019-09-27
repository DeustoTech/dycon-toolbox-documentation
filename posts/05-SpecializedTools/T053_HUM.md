---
layout: default
title: HUM
nav_order: 3
parent: Specialized Tools
MATLAB: T053_HUM

---
```matlab
Nx = 100;
xline = linspace(-1,1,Nx+2);
xline = xline(2:end-1);
dx    = xline(2) - xline(1);
```

```matlab
A = -FEFractionalLaplacian(0.8,1,Nx);
B =  BInterior(xline,-0.3,0.8,'Mass',true);
```

```matlab
idyn            = pde('A',A,'B',B);
idyn.FinalTime  = 0.5;
idyn.Nt         = 100;
idyn.mesh{1}    = xline;
idyn.MassMatrix = MassMatrix(xline);
%%
idyn.InitialCondition = sin(pi*xline');
```

```matlab
iHUM = HUM(idyn);
iHUM.Epsilon = dx^4;
```

```matlab
f0   = zeros(Nx,1);
fOpt = CoConjugateGradient(iHUM,f0,'tol',1e-8);
```


```
    "iter = 0001  |  error = 0.9485"

    "iter = 0002  |  error = 0.66313"

    "iter = 0003  |  error = 0.38735"

    "iter = 0004  |  error = 0.23971"

    "iter = 0005  |  error = 0.19986"

    "iter = 0006  |  error = 0.19191"

    "iter = 0007  |  error = 0.14725"

    "iter = 0008  |  error = 0.090562"

    "iter = 0009  |  error = 0.060476"

    "iter = 0010  |  error = 0.044892"

    "iter = 0011  |  error = 0.19984"

    "iter = 0012  |  error = 0.032607"

    "iter = 0013  |  error = 0.026537"

    "iter = 0014  |  error = 0.020507"

    "iter = 0015  |  error = 0.029467"

    "iter = 0016  |  error = 0.00901"

    "iter = 0017  |  error = 0.0056362"

    "iter = 0018  |  error = 0.002717"

    "iter = 0019  |  error = 0.0079339"

    "iter = 0020  |  error = 0.0087343"

    "iter = 0021  |  error = 0.0012583"

    "iter = 0022  |  error = 0.00073867"

    "iter = 0023  |  error = 0.00046017"

    "iter = 0024  |  error = 0.00040073"

    "iter = 0025  |  error = 0.0018364"

    "iter = 0026  |  error = 0.00016539"

    "iter = 0027  |  error = 0.00035998"

    "iter = 0028  |  error = 7.653e-05"

    "iter = 0029  |  error = 0.0001826"

    "iter = 0030  |  error = 3.1767e-05"

    "iter = 0031  |  error = 3.0045e-05"

    "iter = 0032  |  error = 1.1977e-05"

    "iter = 0033  |  error = 2.4734e-05"

    "iter = 0034  |  error = 4.1429e-06"

    "iter = 0035  |  error = 4.9236e-05"

    "iter = 0036  |  error = 1.7561e-05"

    "iter = 0037  |  error = 4.8916e-06"

    "iter = 0038  |  error = 1.1368e-06"

    "iter = 0039  |  error = 3.4943e-07"

    "iter = 0040  |  error = 6.7376e-07"

    "iter = 0041  |  error = 1.3017e-07"

    "iter = 0042  |  error = 8.5643e-08"

    "iter = 0043  |  error = 1.116e-06"

    "iter = 0044  |  error = 7.1108e-08"

    "iter = 0045  |  error = 1.6954e-08"

    "iter = 0046  |  error = 5.9888e-08"

    "iter = 0047  |  error = 3.051e-09"


```

```matlab
close all
subplot(1,2,1)
surf(iHUM.Dynamics.Control.Numeric)
shading interp
subplot(1,2,2)
surf(iHUM.Dynamics.StateVector.Numeric)
shading interp
```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/05-SpecializedTools/T053/copiaRM_01.png)


```matlab
solve(idyn);
```

```matlab
iHUM.Dynamics.label = 'dynamics';
idyn.label = 'Free';

xx = idyn.FinalTime/5;
```


```


animation([iHUM.Dynamics idyn],'xx',xx,'YLim',[-0.2 0.2],'YLimControl',[-100 100])


```


![]({{site.url}}/{{site.baseurl}}/assets/imgs/05-SpecializedTools/T053/090579.gif)


