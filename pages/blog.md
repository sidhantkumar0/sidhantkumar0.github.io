---
layout: page
title: Blog
permalink: /blog/
position: 4
---

<style>
/* Blog page title only: match the purple used by other titles. */
h1.title { color: #b37eff; }
</style>

{% for post in site.posts %}
  <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
  {% unless forloop.last %}<hr>{% endunless %}
{% else %}
  <p>No posts yet — check back soon.</p>
{% endfor %}
