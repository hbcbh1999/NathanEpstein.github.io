---
layout: view_wide
title:  "Talks & Publications"
date:   2015-12-31 12:00:01
categories: jekyll update, views
img: '../img/cv.png'
---

<div class="col-lg-6 col-sm-12">
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

<div class="col-lg-6 col-sm-12">
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