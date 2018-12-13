---
layout: project
title: "Documentation"
description: A wealth of information is available to help you understand, learn and use the DyCon Toolbox.

---

{::nomarkdown}
<p>
  Below you will find the different classes and functions the DyCon Toolbox offers to help solve problems
  that may show up in real life TOFINISH
</p>
<h1>Classes</h1>
{% for post in site.posts %}
  {% if post.categories[0] contains 'documentation' %}
    {% if post.layout contains 'class' %}
      <hr>
        <div class="post-preview">
          <a href="{{ post.url | prepend: site.baseurl }}">
            <h2 class="post-title">
              &#9673; {{ post.title }}
            </h2>
            <small>
              {{ post.description }}
            </small>
          </a>
        </div>
      <hr>
    {% endif %}
  {% endif %}
{% endfor %}

<h1>Functions</h1>
{% for post in site.posts %}
  {% if post.categories[0] contains 'documentation' %}
    {% if post.layout contains 'function' %}
      <hr>
        <div class="post-preview">
          <a href="{{ post.url | prepend: site.baseurl }}">
            <h2 class="post-title">
              &#9673; {{ post.title }}
            </h2>
            <small>
              {{ post.description }}
            </small>
          </a>
        </div>
      <hr>
    {% endif %}
  {% endif %}
{% endfor %}
{:/nomarkdown}
