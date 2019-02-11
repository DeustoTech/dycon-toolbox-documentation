---
layout: project
title: "Documentation"
description: A wealth of information is available to help you understand, learn and use the DyCon Toolbox.

---
En DyCon Toolbox se ha creado un entorno bajo el paradigma de la programación orientada a objetos. Se ha optado en crear objectos para definir los problemas de optimo control. 

Podemos ver un ejemplo de ello, en el problema de control optimo. Este se define como:

$$ \min_{U \in \Omega} [ \Psi (Y(T),t) + \int_0^T L(Y,U,t)dt] $$

sujeto a:

$$ \dot{Y} = f(t,Y,U) \text{  where } Y(0) = Y_0$$


En la representacion orientado a objetos este problema puede ser representado por el siguiente esquema

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

De esta forma podemos crear distintos algoritmos para resolver el problemas, siguiente siguiendo la misma esctrutura. 
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

Dado que la solucion y la definición del problema tiene la misma estrutura se puede crear facilmente funciones que comparen la precisión de dos algoritmos distintos.

<p>
Classes are abstract objects to facilitate the coding of algorithms, then a list of classes developed in the project
</p>

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
