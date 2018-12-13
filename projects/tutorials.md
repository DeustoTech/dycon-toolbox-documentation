---
layout: project
category: proyect
title: Tutorials
description: Tutorials of the Dycon Toolbox
---

{::nomarkdown}
  {% for topic in site.data.topics %}
    <h1>{{topic[1].name}}</h1>
    <p>{{topic[1].description}}</p>
    <p>See our tutorials:</p>
      <ul>
        {% for post in site.posts %}
          {% if post.categories[1] contains topic[0] and post.layout contains 'tutorial' %}
            <li style="list-style-type:none">
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
            </li>
          {% endif %}
        {% endfor %}
      </ul>
    <hr>
  {% endfor %}
{:/nomarkdown}
