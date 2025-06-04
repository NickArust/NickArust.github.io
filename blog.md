---
layout: default
title: "Blog"
description: "Latest posts and updates."
permalink: /blog/
---

<h2>Blog</h2>
<ul class="post-list">
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url | relative_url }}"><strong>{{ post.title }}</strong></a>
      <span class="post-date">{{ post.date | date: "%B %d, %Y" }}</span>
      <p>{{ post.excerpt | strip_html | truncate: 120 }}</p>
    </li>
  {% endfor %}
</ul>
