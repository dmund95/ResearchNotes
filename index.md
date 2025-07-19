---
layout: default
title: Research Notes
---

# Welcome to My Research Notes

Just a fun way to organize my notes and stay in touch with the latest developments !! 

## Research Topics

<div class="topics-grid">
  {% for topic in site.topics %}
  <div class="topic-card">
    <h3><a href="{{ topic.url | relative_url }}">{{ topic.title }}</a></h3>
    <p>{{ topic.description }}</p>
    <div class="topic-meta">
      <span class="paper-count">{{ topic.papers | size | default: 0 }} papers</span>
    </div>
  </div>
  {% endfor %}
</div>

## Quick Navigation

- [Browse All Topics](/topics/)
- [Recently Added Papers](/recent/)
- [About This Site](/about/)

---

*Last updated: {{ site.time | date: "%B %d, %Y" }}* 