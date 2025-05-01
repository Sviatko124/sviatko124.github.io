---
layout: default
---

<nav style="margin-bottom: 20px;">
  <a href="/" style="margin-right: 15px;">Home</a>
  <a href="/about.html" style="margin-right: 15px;">About</a>
  <a href="https://github.com/sviatko124" target="_blank">GitHub</a>
</nav>

## Latest Posts

<div style="display: flex; overflow-x: auto; padding: 10px; gap: 20px;">

  {% for post in site.posts %}
  <div style="min-width: 250px; border: 1px solid #ccc; padding: 15px; background: #111; border-radius: 8px;">
    <h3 style="margin-top: 0;"><a href="{{ post.url }}" style="color: #0f0;">{{ post.title }}</a></h3>
    <p style="font-size: 0.9em; color: #aaa;">{{ post.date | date: "%B %d, %Y" }}</p>
    <p>{{ post.excerpt | strip_html | truncate: 100 }}</p>
  </div>
  {% endfor %}

</div>
