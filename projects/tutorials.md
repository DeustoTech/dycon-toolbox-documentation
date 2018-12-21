---
layout: project
category: proyect
title: Tutorials
description: Transmitting the results to other researchers, not specialists in control theory, can be difficult. Even among experts on the subject of sharing software is complicated. Here is a series of tutorials for faithful and easy reproduction of mathematical results.
---
 {::nomarkdown}

<p>
  At Dycon Toolbox we have developed some tutorials on the various topics investigated by the DyCon project. These tutorials have been classified for a better organization. Choose the one you prefer and explore.
</p>

 <table>
    <tr>
      <th>Topic</th>
      <th>Description</th>
    </tr>
    {% for topic in site.data.topics %}
    <tr>
      <th>
          <a href="{{site.url}}{{site.baseurl}}/topic/{{topic[0]}}" class="display-block">
              <h4 class="post-title"> {{ topic[1].name }} </h4>
          </a>  
      </th>
      <th>{{topic[1].little_description}}</th>
    </tr>
    {% endfor %}
   <table>

{:/nomarkdown} 






<!-- Codigo Anterior -->
<!-- {::nomarkdown}
  {% for topic in site.data.topics %}
    <div class="post-preview shadowbox">
        <a href="{{site.url}}{{site.baseurl}}/topic/{{topic[0]}}" class="display-block">
            <h3 class="post-title"> {{ topic[1].name }} </h3>
        </a>     
        <p>{{topic[1].little_description}}</p>
    </div>

  {% endfor %}
{:/nomarkdown} -->
