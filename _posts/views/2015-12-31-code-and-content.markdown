---
layout: view_wide
title:  "Code & Content"
date:   2015-12-31 12:00:01
categories: jekyll update, views
img: '../img/projects.png'
---

<div class= "col-lg-4 col-sm-6 col-xs-12">
  <h3>Projects</h3>
  <ul>
    {% for project in site.data.projects %}
      <li class="project">
        <a href="{{project.url}}" target="_blank">
          {{ project.title }}
        </a>
      </li>
    {% endfor %}
  </ul>
</div>

<div class= "col-lg-4 col-sm-6 col-xs-12">
  <h3>Publications</h3>
  <ul>
    {% for writing in site.data.writings %}
      <li class="project">
        <a href="{{writing.url}}" target="_blank">
          {{ writing.title }}
        </a>
      </li>
    {% endfor %}
  </ul>
</div>

<div class= "col-lg-4 col-sm-6 col-xs-12">
  <h3>Talks</h3>
  <ul>
    {% for talk in site.data.talks %}
      <li class="project">
        <a href="{{talk.url}}" target="_blank">
          {{ talk.title }}
        </a>
      </li>
    {% endfor %}
  </ul>
</div>
