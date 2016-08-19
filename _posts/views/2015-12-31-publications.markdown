---
layout: view
title:  "Publications"
date:   2015-12-31 12:00:01
categories: jekyll update, views
img: '../img/writing.png'
---

<ul>
  {% for writing in site.data.writings %}
    <li class="project">
      <a href="{{writing.url}}" target="_blank">
        {{ writing.title }}
      </a>
    </li>
  {% endfor %}
</ul>


