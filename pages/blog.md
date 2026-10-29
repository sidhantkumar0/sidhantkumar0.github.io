---
layout: page
title: Blog
permalink: /blog/
position: 4
---

<style>
/* Blog page title only: match the purple used by other titles. */
h1.title { color: #b37eff; }
/* Post date under each listing title: small, muted, snug under its title. */
.blog-entry h2 { margin-bottom: 0.25rem; }
.blog-date { color: var(--meta); font-size: 0.9em; margin: 0 0 1.25rem; }
/* Divider between posts: quiet 1px line that stays out of the way of the page background. */
hr { border: none; height: 1px; background: #2e3742; }
</style>

{% for post in site.posts %}
  <div class="blog-entry">
    <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
    <p class="blog-date">{{ post.date | date: "%B %-d, %Y" }}</p>
  </div>
  {% unless forloop.last %}<hr>{% endunless %}
{% else %}
  <p>No posts yet — check back soon.</p>
{% endfor %}
