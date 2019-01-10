---
layout: project
title: "Documentation"
description: A wealth of information is available to help you understand, learn and use the DyCon Toolbox.

---

{::nomarkdown}
<!-- <p>
  Below you will find the different classes and functions the DyCon Toolbox offers to help solve problems
  that may show up in real life TOFINISH
</p> -->
<!-- TODO: Index of Content with links to scroll smoothly-->


<!-- <h1 class="doc-header-title">Functions</h1>
<p>
List of functions developed within the framework of the DyCon project. Here below we can find the technical description of each function.
</p>

{% assign qposts = site.posts | where:"layout","function"|sort %}

 <table>
    <tr>
      <th>Name</th>
      <th>Description</th>
    </tr>
    {% for post in qposts %}
        <tr>
          <th><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></th>
          <th>{{ post.data.description }}</th>
        </tr>
    {% endfor %}
 </table>


<h1 class="doc-header-title">Classes</h1> -->
<p>
Classes are abstract objects to facilitate the coding of algorithms, then a list of classes developed in the project
</p>

{% assign qposts = site.posts | where:"layout","class"|sort %}

 <table>
    <tr>
      <th>Name</th>
      <th>Description</th>
    </tr>
    {% for post in qposts %}
        <tr>
          <th><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></th>
          <th>{{ post.description }}</th>
        </tr>
    {% endfor %}
 </table>


{:/nomarkdown}


<!-- 
{% for post in site.posts %}
  {% if post.categories[0] contains 'documentation' and post.layout contains 'function' %}
    <div class="post-preview shadowbox doc-preview-box">
      <a href="{{ post.url | prepend: site.baseurl }}">
        <h3 class="post-preview-title">
          {{ post.title }}(...)
        </h3>
      </a>
      <p>
        {{ post.data.description }}
      </p>
      <a href="{{ post.url | prepend: site.baseurl }}">
        <span>See more...</span>
      </a>
    </div>
  {% endif %}
{% endfor %}

<h1 class="doc-header-title">Classes</h1>
<p>
Classes are abstract objects to facilitate the coding of algorithms, then a list of classes developed in the project
</p>
{% for post in site.posts %}
  {% if post.categories[0] contains 'documentation' and post.layout contains 'class' %}
    <div class="post-preview shadowbox doc-preview-box">
      <a href="{{ post.url | prepend: site.baseurl }}">
        <h3 class="post-preview-title">
          {{ post.title }}
        </h3>
      </a>
      <p>
        {{ post.description }}
      </p>
      <a href="{{ post.url | prepend: site.baseurl }}">
        <span>See more...</span>
      </a>
    </div>
  {% endif %}
{% endfor %}
{:/nomarkdown} -->
