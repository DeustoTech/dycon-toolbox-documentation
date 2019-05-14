---
layout: index
---

{::nomarkdown}

<header class="intro-header">
<div class="container">
    <div class="col-md-10 col-md-offset-1">
        <div class="site-heading">
            <img style="padding-top: 100px;"src="{{site.url}}/{{site.baseurl}}/assets/logo_DyConToolbox_v001.png" width="30%" alt="" srcset="">
            <hr class="small">
            <span class="subheading">
              <!--DyCon Toolbox contains tools for the calculation of non-linear control problems.-->
              The MATLAB toolbox developed inside the <a href="https://cmc.deusto.eus/dycon/">DyCon: Dynamic Control ERC</a> research team.
            </span>
            <hr>
        </div>
    </div>
</div>
</header>

{:/nomarkdown}

<p>DyCon Toolbox is a MATLAB library which serves for the calculation of non-linear control problems. It is developed under the paradigm of object-oriented programming: It defines objects that represent control problems studied by <a href="https://cmc.deusto.eus/people/">the research team</a> of the Chair of Computational Mathematics at <a href="http://deustotech.deusto.es/">DeustoTech</a>. For each of these objects, we create different methods for the resolution of problems. In this way, we can easily choose the type of algorithm to solve the problem. For more information, please explore our <a href="{{site.url}}{{site.baseurl}}/projects/01-documentation">documentation section</a>.</p>

<p>For each of these objects, we create different methods for problem resolution. In this way, we can easily choose the type of algorithm to solve the problem. For more information, continue exploring in our <a href="{{site.url}}{{site.baseurl}}/projects/01-documentation">documentation.</a></p>

<h1>Main Features</h1>

<ul>
  <li>
    <h6>Non-linear dynamics</h6>
    Non-linear dynamics is the first implementation in the toolbox. Our idea is to cover general problems in few lines of code.
  </li>
  <li>
    <h6>Symbolic Interface</h6>
      The symbolic interface of matlab makes the definition of problems easier. And in some cases, the problem can be solved analytically.
  </li>
  <li>
    <h6>High order in time</h6>
      In DyCon toolbox, we solve Ordinary differential equations (ODEs) by differents aproximations. You can choose the all Runge-Kutta solver of MATLAB  for example ode45,ode23,ode23tb. It offers the possibility to create your own solvers or even choose your aproximation.
  </li>
  <li>
    <h6>Modular Structure</h6>
        DyCon Toolbox has been designed to easily accept different blocks of code. In this way, you can use another solver of the differential equations or other optimizers in any one programming language and taking advantage of all the interface already created.
  </li>
</ul>

<p class="index-p">

</p>

<p class="index-p">
    <small>The DyCon MATLAB toolkit is developed primarily by the <a href="http://cmc.deusto.eus/">Chair of Computational Mathematics</a>, at <a href="http://deustotech.deusto.es/">DeustoTech</a>. However, we welcome any improvement in the computational platform. Contact the DyCon Toolbox developer team <a href="mailto:dycon-dev-group@deusto.es">dycon-dev-group@deusto.es</a> for more information.</small>  
  </p>
