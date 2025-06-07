---
layout: page
title: Popular Topics
permalink: /tags/
---

{% include categorized-tag-cloud.html %}

{% for tag in site.tags %}
<section id="{{ tag[0] | slugify }}">
  <h2>{{ tag[0] }}</h2>
  <ul class="post-list">
    {% for post in tag[1] %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        <span class="post-date">{{ post.date | date: "%b %d, %Y" }}</span>
      </li>
    {% endfor %}
  </ul>
</section>
{% endfor %}
