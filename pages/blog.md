---
layout: page
title: Blog
permalink: /blog/
subtitle: "Whatever I'm working on"
position: 4
---

{% for post in site.posts %}
  <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
  <p><small>{{ post.date | date: "%B %d, %Y" }}</small></p>
  {{ post.content }}
{% else %}
  <p>No posts yet — check back soon.</p>
{% endfor %}
