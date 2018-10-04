---
layout: project
title: Tutorials
description: "The tutorials of Dycon Platform"
header-img: "img/home-bg.gif"
---

List of MATLAB code examples to learn control in applied mathematics 


{% for post in site.posts %}
{% if post.categories contains page.title %}
<div class="post-preview">
    <a href="{{ post.url | prepend: site.baseurl }}">
        <h2 class="post-title"> {{ post.title }}
        </h2>
        {% if post.subtitle %}
        <h3 class="post-subtitle">
            {{ post.subtitle }}
        </h3>
        {% endif %}

        {{ site.data.members[post.author].name }}

    </a>
</div>
<hr>
{% endif %}
{% endfor %}