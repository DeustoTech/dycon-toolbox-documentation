---
layout: default
title: Examples
nav_order: 5
---
One of the great contributions of DyCon Toolbox are the examples provided by the team of the Chair of Computational Mathematics.  
<hr>
<div style="display: inline-block">
{% for post in site.data.tutorials %}
<div class="card" style="width: 15rem;">
  <img class="card-img-top" src="{{post[1].img}}" alt="Card image cap">
  <div class="card-body">
    <h5 class="card-title"><b>{{ post[1].name }}</b></h5>
    <p class="card-text">{{ post[1].description }}</p>
    <a href="{{post[1].url}}" class="btn btn-light">read more ...</a>
  </div>
</div>
{% endfor %}
</div>



