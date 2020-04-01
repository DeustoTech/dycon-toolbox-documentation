---
layout: default
title: solve 
parent: pde1d
grand_parent: Dynamics definition
nav_order: 1
---



Method to compute the solution of ode.

#### Inputs
<table>
    <tr>
        <th> Name </th>
        <th> Class</th>
        <th> Description </th>
    </tr>
    <tr>
        <td> iode</td>
        <td>
            <font color="red">'ode'</font>
        </td>
        <td>
            ode object that you want solve
        </td>
    </tr>
    <!-- -------- -->
    <tr>
        <td> Ut</td>
        <td>
            <font color="red">'double'</font>
        </td>
        <td>
            control matrix with dimensions:  $length(iode.Control.sym) \times length(iode.tspan)$
        </td>
    </tr>
</table>

#### Outputs 
<table>
    <tr>
        <th> Name </th>
        <th> Class</th>
        <th> Description </th>
    </tr>
    <tr>
        <td> xt</td>
        <td>
            <font color="red">'casadi.DM'</font>
        </td>
        <td>
            Solution matrix of dynamic
        </td>
    </tr>

</table>

Set Initial condition and solve with null control
```matlab
isys.InitialCondition = [1;2];
%%
u0 = ZerosControl(isys);
xt = solve(isys,u0);
```

```matlab
>> xt

xt = 

[[1, 1.04836, 1.11048, 1.18304, 1.26235, 1.34514, 1.42928, 1.51405, 1.6002, 1.68993, 1.78677, 1.89505, 2.01814, 2.15537, 2.30011, 2.44214, 2.57263, 2.68709, 2.78486, 2.86728, 2.93617, 2.99313, 3.03933, 3.07571, 3.10323, 3.12288, 3.1351, 3.13936, 3.1343, 3.1182, 3.08947, 3.04696, 2.99041, 2.92077, 2.8404, 2.75286, 2.66222, 2.57216, 2.4853, 2.40305, 2.3257, 2.25281, 2.18348, 2.11652, 2.05052, 1.98377, 1.91406, 1.83838, 1.7527, 1.65257], 
 [2, 1.96534, 1.94318, 1.93408, 1.93823, 1.95569, 1.9867, 2.03195, 2.09268, 2.17052, 2.26654, 2.37936, 2.50337, 2.62978, 2.75065, 2.86189, 2.96328, 3.05695, 3.14606, 3.23424, 3.32557, 3.42472, 3.53663, 3.66457, 3.80584, 3.94916, 4.07981, 4.18796, 4.27088, 4.33014, 4.36863, 4.38928, 4.39463, 4.38698, 4.36842, 4.34092, 4.3063, 4.26612, 4.22162, 4.17368, 4.12274, 4.06884, 4.01152, 3.9498, 3.88195, 3.80526, 3.71565, 3.60759, 3.47567, 3.31994]]

 >> class(xt)

ans =

    'casadi.DM'
```
