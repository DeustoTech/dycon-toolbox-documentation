---
layout: project
category: proyect
title: Tutorials
description: Transmitting the results to other researchers, not specialists in control theory, can be difficult. Even among experts on the subject of sharing software is complicated. Here is a series of tutorials for faithful and easy reproduction of mathematical results.
---

{::nomarkdown}
  {% for topic in site.data.topics %}
    <h1>{{topic[1].name}}</h1>
    <p>{{topic[1].description}}</p>
    <p>See our tutorials:</p>
        {% for post in site.posts %}
          {% if post.categories[1] contains topic[0] and post.layout contains 'tutorial' %}
              <div class="post-preview shadowbox">
                <a href="{{ post.url | prepend: site.baseurl }}" class="display-block">
                  <h3 class="post-title"> {{ post.title }} </h3>
                </a>
                  <p class="post-subtitle">
                    {{ post.description }}
                  </p>
                  <small style="color:grey">
                    Author(s):
                    {% for aut in post.author %}
                      {{site.data.members[aut].name}}
                    {% endfor %}
                  </small>
                  <!--p>
                    {{post.date | date: "%B %-d, %Y" }}
                  </p-->
              </div>
          {% endif %}
        {% endfor %}
    <hr>
  {% endfor %}
{:/nomarkdown}
