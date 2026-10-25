---
layout: page
title: Blog
permalink: /blog/
subtitle: "Whatever I'm working on"
position: 4
---

<style>
/* Blog page titles only: match the purple used by other titles. */
h1.title { color: #b37eff; }
h2 a, h2 a:visited,
.post-content h2 a, .post-content h2 a:visited { color: #b37eff; }
.post-content h2 a:visited { filter: none; }
</style>

{% for post in site.posts %}
  <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
{% else %}
  <p>No posts yet — check back soon.</p>
{% endfor %}
