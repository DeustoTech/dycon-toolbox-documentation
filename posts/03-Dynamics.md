---
layout: default
title: Dynamics Definition
nav_order: 3
has_children: true
---

{::nomarkdown}  
<h4 id="ToC">Table of Contents</h4  >
<ol>
{% for class in site.data.DynamicClass %}
    <li><b><a href="#{{class[0]}}">{{class[0]}}</a></b>. {{class[1].description}}</li>
    <h5>Methods</h5>
    <ul>
    {% for method in class[1].methods %}
        <li><a href="#{{class[0]}}{{method[0]}}">{{method[0]}}</a></li>
    {% endfor %}
    </ul>
    <p> </p>
{% endfor %}
</ol>

{% for class in site.data.DynamicClass %}
    <hr>
    <div style="border: 2px solid red;padding:2px">
    <div id="{{class[0]}}"><h1><b style="color:red">Class:: </b><b>{{class[0]}}</b ></h1></div>
    <p>{{class[1].description}}</p>
    <!-- BUCLE METHODS -->
    {% for method in class[1].methods %}
        <div id="{{class[0]}}{{method[0]}}" style="border: 1px solid blue;padding:2px">
            <div style="display:flex">
                <div style="padding-left:auto; width: 100%;" >
                    <h3 ><b style="color:blue">Method::</b><b>{{method[0]}}</b> of <b style="color:red">Class::</b><b>{{class[0]}}</b></h3>
                </div>
                <div style="padding-left:auto; width: 100%;" >
                    <p style="text-align: right;"><a href="">Index&#10548;</a></p>
                </div>
            </div>
            <!-- SYNTAX -->
            <h4>Syntax</h4>
            <ul>
            {% for syntax in method[1].syntaxis %}
                <li><code>
                {{syntax[1]}}
                </code></li>
            {% endfor %}
            </ul>
            <!-- INTERFACE -->
            <h4>Interface</h4>
            <div style="display:block" align="center" vertical-align="top">
                <div style="padding:5px">
                    <table align="center">
                        <tr>
                            <th style="text-align:center;background-color:#92354f93"colspan="3">INPUTS</th>
                        </tr>
                        <tr>
                            <th>Name</th>
                            <th>Class</th>
                            <th>Description</th>
                        </tr>
                        {% for input in method[1].inputs %}
                        <tr>
                            <td>{{input[0]}}</td>
                            <td><a href="{{input[1].url_class}}">{{input[1].class}}</a></td>           
                            <td>{{input[1].description|markdownify}}</td>
                        </tr>
                        {% endfor%}
                    </table>
                </div>
                {% if  method[1].outputs %}
                <div style="padding:10px">
                    <table>
                        <tr>
                            <th style="background-color:#92354f93;text-align:center"colspan="3">OUTPUTS</th>
                        </tr>
                        <tr>
                            <th>Name</th>
                            <th>Class</th>
                            <th>Description</th>
                        </tr>
                        {% for output in method[1].outputs %}
                        <tr>
                            <td>{{output[0]}}</td>
                            <td><a href="{{output[1].url_class}}">{{output[1].class}}</a></td>
                            <td>{{output[1].description}}</td>
                        </tr>
                        {% endfor%}
                    </table>
                </div>
                {% endif %}
            </div>
            <!-- EXAMPLES -->
            {% assign exp1 = method[0] | append: ".md" |prepend:"/"| prepend: {{class[0]}} | prepend:"examples/"%}         
            {% capture my_include %}{% include {{exp1}} %}{% endcapture %}
            <h4>Example</h4>
            {{ my_include | markdownify }}
    </div>
    {% endfor %}
    </div>
    <hr>
{% endfor %}
{:/nomarkdown}
 