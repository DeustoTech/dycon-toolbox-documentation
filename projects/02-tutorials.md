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
