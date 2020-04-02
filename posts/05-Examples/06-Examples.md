---
layout: default
nav_order: 5
title: Examples
---
<p>
One of the great contributions of DyCon Toolbox are the examples provided by the team of the Chair of Computational Mathematics. These examples are on the  <a href="https://deustotech.github.io/DyCon-Blog/">DyCon Blog</a> web platform, where the <a href="https://cmc.deusto.eus/">Chair of Computational Mathematics</a> team publish different software tutorials including DyCon toolbox tutorials.
</p>
<hr>
<div class="separator"></div>
<div id="post-cards">
  {% for post in site.data.tutorials %}
    <center>
    <div class="card">
      <img width="50%" src="{{post[1].img}}" alt="">
      <div class="card-body">
        <h3 class="card-title"><b>{{ post[1].name }}</b></h3>
        <p class="card-text">{{ post[1].description }}</p>
        <a href="{{post[1].url}}" class="btn btn-light">read more</a>
      </div>
    </div>
    </center>
  {% endfor %}






