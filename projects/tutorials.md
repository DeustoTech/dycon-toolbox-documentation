---
layout: project
category: proyect
title: Tutorials
description: Tutorials of the Dycon Toolbox
---


{% for topic in site.data.topics %}
  <h1>{{topic[1].name}}</h1>
  <p>{{topic[1].description}}</p>
  <p>See our tutorials:</p>
  <div id="wrapper" class="shadowbox">
    <ul>
      {% for post in site.posts %}
        {% if post.categories[1] contains topic[0] and post.layout contains 'tutorial' %}
          <li style="list-style-type:none">
            <div class="post-preview">
              <a href="{{ post.url | prepend: site.baseurl }}" class="display-block">
                <p class="post-title"> &#9673; {{ post.title }} <small><p class="post-subtitle">{{ post.description }}</p></small></p>
                  <small style="color:grey">
                    {% for aut in post.author %}
                      &#9702; {{site.data.members[aut].name}}
                    {% endfor %}
                  </small>
                <p>
                  {{post.date | date: "%B %-d, %Y" }}
                </p>
              </a>
            </div>
          </li>
        {% endif %}
      {% endfor %}
    </ul>
  </div>
  <hr>
{% endfor %}
