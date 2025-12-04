---
layout: page
title: Blog
permalink: /blog/
description: Thoughts on research, technology, and life
nav: false
nav_order: 4
pagination:
  enabled: true
  collection: posts
  permalink: /page/:num/
  per_page: 5
  sort_field: date
  sort_reverse: true
---

<div class="post-list">
  {% for post in paginator.posts %}
  <article class="post-preview">
    <a href="{{ post.url | relative_url }}">
      <h2 class="post-title">{{ post.title }}</h2>
    </a>
    <p class="post-meta">
      {{ post.date | date: "%B %-d, %Y" }}
      {% if post.author %} • {{ post.author }}{% endif %}
    </p>
    <p class="post-excerpt">
      {% if post.description %}
        {{ post.description }}
      {% else %}
        {{ post.content | strip_html | truncatewords: 50 }}
      {% endif %}
    </p>
    <div class="post-tags">
      {% for tag in post.tags %}
        <a href="{{ '/blog/tag/' | append: tag | relative_url }}" class="badge badge-secondary">{{ tag }}</a>
      {% endfor %}
    </div>
    <hr>
  </article>
  {% endfor %}
</div>

{% if paginator.total_pages > 1 %}

<nav aria-label="Page navigation">
  <ul class="pagination justify-content-center">
    {% if paginator.previous_page %}
    <li class="page-item">
      <a class="page-link" href="{{ paginator.previous_page_path | relative_url }}">&laquo; Prev</a>
    </li>
    {% endif %}
    
    {% for page in (1..paginator.total_pages) %}
    <li class="page-item {% if page == paginator.page %}active{% endif %}">
      {% if page == 1 %}
      <a class="page-link" href="{{ '/blog/' | relative_url }}">{{ page }}</a>
      {% else %}
      <a class="page-link" href="{{ '/blog/page/' | append: page | relative_url }}">{{ page }}</a>
      {% endif %}
    </li>
    {% endfor %}
    
    {% if paginator.next_page %}
    <li class="page-item">
      <a class="page-link" href="{{ paginator.next_page_path | relative_url }}">Next &raquo;</a>
    </li>
    {% endif %}
  </ul>
</nav>
{% endif %}
