---
layout: default
title: SetIntegrator 
parent: pde1d
grand_parent: Dynamics definition
nav_order: 1
---

#### Mandatory Inputs
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
        <td>method</td>
        <td>
            <font color="red">'double'</font>
        </td>
        <td>This is the integrator method. This parameter must be member of this:
            {"casadi","BackwardEuler","RK4","LinearFordwardEuler","SemiLinearFordwardEuler"}
        </td>
    </tr>
</table>

 Method parameter is a  procedure for solving ordinary differential equations (ODEs) with a given initial value.

   1. casadi
   2. BackwardEuler
   3. RK4
   4. LinearFordwardEuler
   5. SemiLinearFordwardEuler