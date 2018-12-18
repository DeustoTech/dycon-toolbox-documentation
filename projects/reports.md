---
layout: project
title: Reports
description: Collections of contributions of all members of Chair of Computational Mathematics
---

{::nomarkdown}

<!-- TODO: Index of Content with links to scroll smoothly-->
{% for post in site.posts %}
  {% if post.categories[0] contains 'report' and post.layout contains 'report' %}
  <div class="post-preview shadowbox doc-preview-box">
    <a href="{{ post.url | prepend: site.baseurl }}">
      <h3 class="post-preview-title">
        {{ post.title }}
      </h3>
    </a>
    <p>{{site.data.members[post.author].name}} - {{post.date|date_to_long_string}}</p>
    <p>{{ post.description }}</p>
    <a href="{{ post.url | prepend: site.baseurl }}">
      <span>See more...</span>
    </a>
  </div>
  {% endif %} 
{% endfor %}

{:/nomarkdown}
