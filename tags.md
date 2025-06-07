---
layout: page
title: Blog Tags
permalink: /tags/
---

<div id="tag-cloud">
  {% include tag-cloud.html %}
</div>

{% for tag in site.tags %}
<section id="{{ tag[0] | slugify }}" class="tag-section">
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
