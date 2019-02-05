---
layout: index
---

{::nomarkdown}

<header class="intro-header">
<div class="container">
    <div class="col-md-10 col-md-offset-1">
        <div class="site-heading">
            <img style="padding-top: 100px;"src="{{site.url}}/{{site.baseurl}}/assets/logo_DyConToolbox_v001.png" width="40%" alt="" srcset="">
            <hr class="small">
            <span class="subheading">
              DyCon Toolbox is a package for MATLAB dedicated to the resolution of control problems.
            </span>
            <hr>
        </div>
    </div>
</div>
</header>

{:/nomarkdown}

      
  DyCon Toolbox solve the following problem :

  $$\min_{u \in \Omega} [ \Psi(t,Y(T)) + \int_0^T L(t,Y,U) dt ]
  \ \text{     with: }
    \dot{Y} = f(t,Y,U)$$


<table align="center" width="50%">
                    <tbody><tr>
                        <td>    


<div class="language-matlab highlighter-rouge"><div class="highlight"><pre class="highlight"><code><span class="c1">% define the state and control</span>
<span class="n">Y</span> <span class="o">=</span> <span class="n">sym</span><span class="p">(</span><span class="s1">'y'</span><span class="p">,[</span><span class="mi">2</span> <span class="mi">1</span><span class="p">]);</span> <span class="n">U</span> <span class="o">=</span> <span class="n">sym</span><span class="p">(</span><span class="s1">'u'</span><span class="p">,[</span><span class="mi">2</span> <span class="mi">1</span><span class="p">]);</span>
<span class="c1">% define your wierd dynamics</span>
<span class="n">F</span> <span class="o">=</span> <span class="p">[</span> <span class="n">Y</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span><span class="o">*</span><span class="n">Y</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span> <span class="o">+</span> <span class="n">U</span><span class="p">(</span><span class="mi">1</span><span class="p">)</span>        <span class="p">;</span> <span class="k">...</span>
      <span class="n">Y</span><span class="p">(</span><span class="mi">2</span><span class="p">)</span>      <span class="o">+</span> <span class="nb">sin</span><span class="p">(</span><span class="n">U</span><span class="p">(</span><span class="mi">2</span><span class="p">))</span> <span class="p">]</span> <span class="p">;</span>
<span class="n">dynamics</span> <span class="o">=</span> <span class="n">ode</span><span class="p">(</span><span class="n">F</span><span class="p">,</span><span class="n">Y</span><span class="p">,</span><span class="n">U</span><span class="p">);</span>
<span class="n">dynamics</span><span class="o">.</span><span class="n">Condition</span> <span class="o">=</span> <span class="p">[</span><span class="mi">1</span><span class="p">;</span><span class="mi">1</span><span class="p">];</span>
<span class="c1">% define your functional with Y and U simbolic vars </span>
<span class="n">Psi</span> <span class="o">=</span> <span class="n">Y</span><span class="o">.'*</span><span class="n">Y</span><span class="p">;</span> 
<span class="n">L</span>   <span class="o">=</span> <span class="mf">0.001</span><span class="o">*</span> <span class="n">U</span><span class="o">.'*</span><span class="n">U</span><span class="p">;</span>
<span class="c1">% Create a OptimalControl Object </span>
<span class="n">iP</span> <span class="o">=</span> <span class="n">OptimalControl</span><span class="p">(</span><span class="n">dynamics</span><span class="p">,</span><span class="n">Psi</span><span class="p">,</span><span class="n">L</span><span class="p">);</span>
<span class="c1">% And Solve </span>
<span class="n">GradientMethod</span><span class="p">(</span><span class="n">iP</span><span class="p">,</span><span class="s1">'Graphs'</span><span class="p">,</span><span class="nb">true</span><span class="p">)</span>
</code></pre></div></div>

<div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>    Solve with presicion: 

    Solve with presicion: 

        We obtain: J(u) = 1.516010E+00

        mean(||dJ_i||^2) = 7.123165E-03

    With 15 iterations,     In 3.4525 seconds

</code></pre></div></div>

  </td>
  <td><img src="assets/portada.jpg" width="600" alt=""></td>

</tr>
</tbody></table>


<h1>Main Features</h1>
<ul>
  <li>
    <h3>Symbolic Interface</h3> 
    This toolbox uses the
  </li>
  <li>
    <h3>Non-linear dynamics</h3>
      Non-linear dynamics is the first implementation in the toolbox. Our idea is to cover very general problems in a few lines of code.
      <!-- <p><a href="{{site.url}}{{site.baseurl}}/tutorial/tp02/T0008">see more...</a></p>  -->

  </li>
  <li>
    <h3>Scalable</h3>
      This Toolbox is a container of different optimization algorithms, where new methods can be developed within a structure already built and with reusable functions, for the comparison of results.
  </li>

</ul>
<p class="index-p">
  </p>

<p class="index-p">
    <small>The DyCon MATLAB toolkit is developed primarily by the Chair of Computational Mathematics, at DeustoTech. However, we welcome any improvement in the computational platform. Contact the DyCon Toolbox developer team dycon-dev-group@deusto.es for more information.</small>  
  </p>
