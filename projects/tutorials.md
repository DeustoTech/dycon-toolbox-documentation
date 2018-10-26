---
layout: project
title: Tutorials
description: "The tutorials of Dycon Platform"
header-img: "img/home-bg.gif"
---

<!-- {% for WP in site.data.WP%}
<hr>
<h1>{{WP[1].name}}</h1>
<hr>

<ul>
{% for post in site.posts %}
{% if post.categories contains page.title %}

{% if post.WP == WP[0] %}
<li>
<div class="post-preview">
    <a href="{{ post.url | prepend: site.baseurl }}" style="display: block">
        <p class="post-title"> {{ post.title }}
        </p>
        {% if post.subtitle %}
        <small><p class="post-subtitle">{{ post.subtitle }}</p></small> 
        {% endif %}

        {{ site.data.members[post.author].name }}
    </a>
</div>
</li>

{% endif %}
{% endif %}
{% endfor %}
</ul>
{% endfor %}  -->




<ul>
{% for post in site.posts %}
{% if post.categories contains page.title %}
<hr>
<li style="list-style-type:none">
    <div class="post-preview">
            <a href="{{ post.url | prepend: site.baseurl }}" style="display: block">
            <p class="post-title"> &#9673; {{ post.title }} <small><p class="post-subtitle">{{ post.subtitle }}</p></small></p>
                <small style="color:grey">
                            {% for aut in post.author %}
                            &#9702; {{site.data.members[\'aut\'].name}} 
                            {% endfor %}
                </small>
            <p>{{post.date | date: "%B %-d, %Y" }}</p>    
            </a>
    </div>
</li>
<hr>
{% endif %}
{% endfor %}
</ul> 
