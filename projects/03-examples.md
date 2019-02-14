---
layout: project
category: proyect
title: Examples
description: Here you can find some examples of using DyCon Toolbox
---
 {::nomarkdown}

 <table style="text-align:center;">
    <tr>
      <th>Topic</th>
      <th>Description</th>
      <th>Nº of examples</th>

    </tr>
    {% for topic in site.data.examples %}
    <tr>
      <th>
          <a href="{{site.url}}{{site.baseurl}}/example/{{topic[0]}}" class="display-block">
                {%- assign qposts = site.posts | where:"layout","example" -%}
                {%- assign qposts = qposts | where:"categories",topic[0] -%}
              <h4 class="post-title">{{topic[1].name}}</h4>
          </a>  
      </th>
      <th>{{topic[1].little_description}}</th>
      <th>[<small>{{ qposts | size }}</small>]</th>
    </tr>
    {% endfor %}
   <table>

{:/nomarkdown} 
