---
layout: default
title: Browse Topics
permalink: /topics/
---

<div class="main-container">
    <div class="left-column">
        <section class="tag-cloud-section">
            <h2>🏷️ Browse All Topics</h2>
            
            <div class="tag-cloud">
                <div class="tag-list">
                    {% assign sorted_tags = site.tags | sort: 'size' | reverse %}
                    {% for tag in sorted_tags %}
                    <a href="#{{ tag[0] | slugify }}" class="tag-item tag-size-3">
                        {{ tag[0] | replace: '-', ' ' | capitalize }} ({{ tag[1].size }})
                    </a>
                    {% endfor %}
                </div>
            </div>
            
            <div style="margin-top: 3rem;">
                <h2>📡 Articles by Topic</h2>
                
                {% assign sorted_tags = site.tags | sort %}
                {% for tag in sorted_tags %}
                <div id="{{ tag[0] | slugify }}" class="tag-section">
                    <h3 class="tag-section-title">
                        {{ tag[0] | replace: '-', ' ' | capitalize }}
                        <span class="tag-count">({{ tag[1] | size }})</span>
                    </h3>
                    
                    {% for post in tag[1] %}
                    <div class="tag-article">
                        <a href="{{ post.url | relative_url }}" class="tag-article-link">
                            <span class="article-category">{{ post.category_display | default: post.categories[0] | capitalize }}</span>
                            <span class="article-title">{{ post.title }}</span>
                            <span class="article-date">{{ post.date | date: "%b %Y" }}</span>
                        </a>
                    </div>
                    {% endfor %}
                </div>
                {% endfor %}
            </div>
        </section>
    </div>
    
    <aside class="author-bio-sidebar">
        <h3 style="color: #00d4ff; margin-bottom: 1rem;">Topic Stats</h3>
        <div class="stats-grid">
            <div class="stat-item">
                <div class="stat-number">{{ site.tags | size }}</div>
                <div class="stat-label">Topics</div>
            </div>
            <div class="stat-item">
                <div class="stat-number">{{ site.posts | size }}</div>
                <div class="stat-label">Articles</div>
            </div>
        </div>
    </aside>
</div>
