---
layout: project
category: proyect
title: Examples
description: Transmitting the results to other researchers, not specialists in control theory, can be difficult. Even among experts on the subject of sharing software is complicated. Here is a series of tutorials for faithful and easy reproduction of mathematical results.
---
 {::nomarkdown}

<p>
  At Dycon Toolbox we have developed some tutorials on the various topics investigated by the DyCon project. These tutorials have been classified for a better organization. Choose the one you prefer and explore.
</p>

 <table style="text-align:center;">
    <tr>
      <th>Topic</th>
      <th>Description</th>
      <th>Nº of Tutorials</th>

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
