---
layout: project
title: "Documentation"
description: "Scheme under which control problems are developed."

---
Dycon Toolbox is an environment under the paradigm of object-oriented programming. We create objects to define control problems. We can see an example of this in a general optimal control problem: 

$$ \min_{U \in \Omega} [ \Psi (Y(T),t) + \int_0^T L(Y,U,t)dt] $$

subject to:

$$ \dot{Y} = f(t,Y,U) \text{  where } Y(0) = Y_0$$


In object-oriented programming, this problem can be described through the following scheme:

<div style="text-align: center;">
{% mermaid %}
graph TB
    OC["OptimalControl<br>Object"]
    OC --> ode
    OC --> psi["Symbolic<br>expression of Psi"]
    OC --> L["Symbolic<br>expression of L"]

    ode["ode<br>Object"]
    ode --> odep1["Dynamic<br>Equation"]
    ode --> odep2["Initial<br>Condition"]

{% endmermaid %}
</div>
{::nomarkdown}

In this way, we can create algorithms to solve different problems following the same underneath structure, and the solutions of those problems are independent on the solver employed. 

<div style="text-align: center;">
{% mermaid %}
graph TB
    OC["OptimalControl<br>Object"]
    CG["Algorithm"]
    sol["solution"]
    plus["+"]

    CG --> plus
    OC --> plus

    plus --> sol
{% endmermaid %}
</div>

Therefore, we can easily create functions able to compare the accuracy of distinct methods and algorithms.

<h2> Classes </h2>
Below we can see the classes defined within DyCon Toolbox.

{% assign qposts = site.posts | where:"layout","class"|sort: 'number'%}

 <table>
    <tr>
      <th>Name</th>
      <th>Description</th>
    </tr>
    {% for post in qposts %}
        <tr>
          <th><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></th>
          <th>{{ post.description }}</th>
        </tr>
    {% endfor %}
 </table>


{:/nomarkdown}
