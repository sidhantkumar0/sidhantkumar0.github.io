---
layout: page
title: Sidhant Kumar
hide: true
---

<div class="home-hero">
  <img class="home-logo" src="{{ 'assets/avatar.png' | relative_url }}" alt="Sidhant Kumar logo">
  <p class="home-tagline">Recent Network Technology grad building a homelab and documenting the journey.</p>
  <div class="home-cta">
    <a class="home-btn" href="{{ '/projects/' | relative_url }}">View Projects</a>
    <a class="home-btn home-btn-secondary" href="{{ '/assets/Sidhant%20Kumar%20Resume.pdf' | relative_url }}">Download Resume</a>
  </div>
</div>

## Featured Projects

<div class="home-featured">
  {% for project in site.portfolio limit:3 %}
  <a class="home-card" href="{{ project.url | relative_url }}">
    {% if project.img %}
    <img src="{{ project.img | relative_url }}" alt="{{ project.title }}">
    {% endif %}
    <span class="home-card-title">{{ project.title }}</span>
  </a>
  {% endfor %}
</div>

[View all projects]({{ '/projects/' | relative_url }})

## Latest Post

{% assign latest_post = site.posts | first %}
{% if latest_post %}
### [{{ latest_post.title }}]({{ latest_post.url | relative_url }})

{{ latest_post.date | date: "%B %d, %Y" }}

{{ latest_post.excerpt | strip_html | truncatewords: 30 }}
{% else %}
No posts yet — check back soon.
{% endif %}
