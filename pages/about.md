---
layout: page
title: About Me
permalink: /about/
position: 1
---

<style>
/* ---- About page motion ---- */
.about-greeting {
  font-size: 1.9rem;
  line-height: 1.3;
  margin-bottom: 0.25rem;
}
.typing-cursor {
  display: inline-block;
  color: #22d3ee;
  animation: about-blink 1.05s steps(1) infinite;
  font-weight: 300;
}
@keyframes about-blink {
  50% { opacity: 0; }
}
.about-lede {
  font-size: 1.15rem;
  margin-top: 0;
}
/* Scroll reveal: hidden only when JS is running, so no-JS still shows everything */
html.js .reveal {
  opacity: 0;
  transform: translateY(26px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}
html.js .reveal.visible {
  opacity: 1;
  transform: none;
}
@media (prefers-reduced-motion: reduce) {
  html.js .reveal { opacity: 1; transform: none; transition: none; }
  .typing-cursor { animation: none; }
}
/* Education timeline */
.about-timeline {
  position: relative;
  margin: 1.5rem 0 1rem;
  padding-left: 1.9rem;
  border-left: 2px solid rgba(255, 255, 255, 0.14);
}
.timeline-item {
  position: relative;
  padding-bottom: 1.6rem;
}
.timeline-item:last-child { padding-bottom: 0.25rem; }
.timeline-dot {
  position: absolute;
  left: calc(-1.9rem - 7px);
  top: 5px;
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: transparent;
  border: 2px solid #22d3ee;
  transition: background 0.6s ease, box-shadow 0.6s ease;
}
.timeline-item.visible .timeline-dot {
  background: #22d3ee;
  box-shadow: 0 0 14px rgba(34, 211, 238, 0.8);
}
.timeline-date {
  display: inline-block;
  font-size: 0.85rem;
  letter-spacing: 0.04em;
  color: #22d3ee;
  margin-bottom: 0.2rem;
}
.timeline-school {
  font-size: 1.1rem;
  margin: 0 0 0.15rem;
}
.timeline-detail {
  margin: 0;
  opacity: 0.85;
}
</style>

<h2 class="about-greeting"><span id="typed-greeting">Hi, I'm Sidhant Kumar,</span><span class="typing-cursor" aria-hidden="true">▍</span></h2>

<div class="reveal about-lede" markdown="1">
with a Bachelor of Information Technology, specializing in Network Technology, from Carleton University, along with an Advanced Diploma in Computer Engineering Technology – Networking from Algonquin College.
</div>

<div class="reveal" markdown="1">
My interests are primarily focused on **networking, infrastructure, systems administration, virtualization, cloud technologies, and cybersecurity**. I enjoy learning how different technologies work together and, more importantly, getting hands-on experience building and troubleshooting them.
</div>

<div class="reveal" markdown="1">
This website is a documentation of that journey.
</div>

<div class="reveal" markdown="1">
I use it to share the projects I work on, the technologies I experiment with, the problems I encounter, and the solutions I develop along the way. Rather than simply documenting the final result, I want to capture the process — **what I was trying to accomplish, how I approached it, what went wrong, how I fixed it, and what I learned from the experience.**
</div>

<div class="reveal" markdown="1">
Many of these projects are part of my personal homelab, where I continue to build practical experience with networking equipment, servers, Raspberry Pis, Kubernetes, virtualization, and other infrastructure technologies.
</div>

<div class="reveal" markdown="1">
My goal is to continuously learn, build, troubleshoot, and improve — while creating a record of that progress that I can look back on and share with others.
</div>

<h2 class="reveal">Education</h2>

<div class="about-timeline">
  <div class="timeline-item reveal">
    <span class="timeline-dot" aria-hidden="true"></span>
    <div class="timeline-date">June 2026</div>
    <div class="timeline-school"><strong>Carleton University</strong></div>
    <p class="timeline-detail">Bachelor of Information Technology, Network Technology</p>
  </div>
  <div class="timeline-item reveal">
    <span class="timeline-dot" aria-hidden="true"></span>
    <div class="timeline-date">June 2026</div>
    <div class="timeline-school"><strong>Algonquin College</strong></div>
    <p class="timeline-detail">Advanced Diploma, Computer Engineering Technology – Networking</p>
  </div>
</div>

<script>
(function() {
  document.documentElement.classList.add('js');

  var reduceMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

  // Typing effect on the greeting (full text is in the HTML, so no-JS still shows it)
  var typed = document.getElementById('typed-greeting');
  if (typed && !reduceMotion) {
    var full = typed.textContent;
    typed.textContent = '';
    var i = 0;
    (function type() {
      if (i <= full.length) {
        typed.textContent = full.slice(0, i);
        i++;
        setTimeout(type, 45);
      }
    })();
  }

  // Scroll reveal
  var revealEls = document.querySelectorAll('.reveal');
  if ('IntersectionObserver' in window && !reduceMotion) {
    var observer = new IntersectionObserver(function(entries) {
      entries.forEach(function(entry) {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible');
          observer.unobserve(entry.target);
        }
      });
    }, { threshold: 0.12 });
    revealEls.forEach(function(el) { observer.observe(el); });
  } else {
    revealEls.forEach(function(el) { el.classList.add('visible'); });
  }
})();
</script>
