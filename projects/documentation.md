---
layout: project
title: "Documentation"
description: "Documentation of Dycon Platform functions and classes"
---
{% for post in site.posts %}
{% if post.categories[0] contains 'documentation' %}
<hr>
<div class="post-preview">
    <a href="{{ post.url | prepend: site.baseurl }}">
        <h2 class="post-title"> &#9673; {{ post.title }}
        </h2>
        {% if post.subtitle %}
        <h3 class="post-subtitle">
            {{ post.subtitle }}
        </h3>
        {% endif %}
        <small>
        <p>{{ site.data.members[post.author].name }}</p>
        {{ post.short_description }}
        </small>

    </a>
</div>
<hr>
{% endif %}
{% endfor %}
