---
layout: project
category: proyect
title: Tutorials
description: "The tutorials of Dycon Platform"
---


{% for topic in site.data.topics %}
<h1>{{topic[1].name}}</h1>
<p>{{topic[1].description}}</p>


<div id="wrapper">
<ul>
{% for post in site.posts %}
{% if post.categories[1] contains topic[0] %}
{% if post.layout contains 'tutorial' %}
<hr>
<li style="list-style-type:none">
    <div  class="post-preview">
            <a href="{{ post.url | prepend: site.baseurl }}" style="display: block">
            <p class="post-title"> &#9673; {{ post.title }} <small><p class="post-subtitle">{{ post.subtitle }}</p></small></p>
                <small style="color:grey">
                            {% for aut in post.author %}
                            &#9702; {{site.data.members[\"aut\"].name}} 
                            {% endfor %}
                </small>
            <p>{{post.date | date: "%B %-d, %Y" }}</p>    
            </a>
    </div>
</li>
<hr>
{% endif %}
{% endif %}
{% endfor %}
</ul> 
</div>

{% endfor %}
