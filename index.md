---
layout: main
title: Blog
---

<ul class="artical-list">
  {% for post in site.categories.blog %}
  <li>
    <a href="{{ post.url }}" class="title">{{ post.title }}</a>
    <div class="title-desc">{{ post.description }}</div>
  </li>
  {% endfor %}
</ul>