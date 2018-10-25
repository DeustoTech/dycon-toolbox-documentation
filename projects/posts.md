---
layout: project
title: Posts
description: "Divulgative concepts of control problems in real life"
header-img: "img/home-bg.gif"
---


<ul>
{% for post in site.posts %}
{% if post.categories contains page.title %}

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
{% endfor %}
</ul> 
