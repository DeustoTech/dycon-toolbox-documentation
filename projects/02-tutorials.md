---
layout: project
category: proyect
title: First Steps
description: Here you will find the first tutorials to understand the basic concepts of DyCon Toolbox.
---
 {::nomarkdown}

    {% for topic in site.data.tutorials %}

      {%- assign qposts = site.posts | where:"layout","tutorial" -%}
      {%- assign qposts = qposts | where:"categories",topic[0]|sort: 'number' -%}
        <h3 class="post-title">{{topic[1].name}}</h3>
        {{topic[1].little_description}}

        {% for post in qposts %}
            <div class="shadowbox">
            <a href="{{site.url}}{{site.baseurl}}{{post.url}}"><h4>{{post.title}}</h4></a>
            <p>{{post.description}}</p>
            </div>
        {% endfor %}

    {% endfor %}

{:/nomarkdown} 






<!-- Codigo Anterior -->
<!-- {::nomarkdown}
  {% for topic in site.data.topics %}
    <div class="post-preview shadowbox">
        <a href="{{site.url}}{{site.baseurl}}/topic/{{topic[0]}}" class="display-block">
            <h3 class="post-title"> {{ topic[1].name }} </h3>
        </a>     
        <p>{{topic[1].little_description}}</p>
    </div>

  {% endfor %}
{:/nomarkdown} -->
