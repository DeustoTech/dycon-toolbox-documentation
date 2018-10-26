---
layout: project
title: Posts
description: ""
header-img: "img/home-bg.gif"
---

<h1> Divulgative concepts of control problems in real life </h1>
<ul>
{% for post in site.posts %}
{% if post.categories contains page.title %}
{% if post.difficulty == 'Easy'  %}

<li style="list-style-type:none">
    <div class="post-preview">
            <a href="{{ post.url | prepend: site.baseurl }}" style="display: block">
            <p class="post-title"> &#9673; {{ post.title }} <small><p class="post-subtitle">{{ post.subtitle }}</p></small></p>
                <small style="color:grey">
                {% for author in site.data.members %}
                        {% if post.author contains author[0] %}
                            &#9702; {{author[1].name}} 
                        {% endif %}
                {% endfor %}
                </small>
            <p>{{post.date | date: "%B %-d, %Y" }}</p>    
            </a>
    </div>
</li>
{% endif %}
{% endif %}
{% endfor %}
</ul> 



<h1> Hard Mathematical Concepts  </h1>
<ul>

{% for post in site.posts %}
{% if post.categories contains page.title %}
{% if post.difficulty == 'Hard' %}

<li style="list-style-type:none">
    <div class="post-preview">
            <a href="{{ post.url | prepend: site.baseurl }}" style="display: block">
            <p class="post-title"> &#9673; {{ post.title }} <small><p class="post-subtitle">{{ post.subtitle }}</p></small></p>
                <small style="color:grey">
                {% for author in site.data.members %}
                        {% if post.author contains author[0] %}
                            &#9702; {{author[1].name}} 
                        {% endif %}
                {% endfor %}
                </small>
            <p>{{post.date | date: "%B %-d, %Y" }}</p>    
            </a>
    </div>
</li>
{% endif %}
{% endif %}
{% endfor %}
</ul> 