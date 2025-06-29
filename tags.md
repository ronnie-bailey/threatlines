---
layout: default
title: All Topics
permalink: /tags/
---

<div class="main-container">
    <div class="left-column">
        <section class="tag-cloud-section">
            <h2>🏷️ All Topics</h2>
            
            <div class="tag-cloud">
                <div class="tag-list">
                    {% assign sorted_tags = site.tags | sort: 'size' | reverse %}
                    {% for tag in sorted_tags %}
                    {% assign tag_size_class = 'tag-size-1' %}
                    {% if tag[1].size >= 5 %}
                        {% assign tag_size_class = 'tag-size-4' %}
                    {% elsif tag[1].size >= 3 %}
                        {% assign tag_size_class = 'tag-size-3' %}
                    {% elsif tag[1].size >= 2 %}
                        {% assign tag_size_class = 'tag-size-2' %}
                    {% endif %}
                    
                    <a href="#{{ tag[0] | slugify }}" class="tag-item {{ tag_size_class }}" title="{{ tag[1].size }} articles">
                        {{ tag[0] | replace: '-', ' ' | capitalize }} ({{ tag[1].size }})
                    </a>
                    {% endfor %}
                </div>
            </div>
            
            <div style="margin-top: 3rem;">
                <h2>📡 Browse Articles by Topic</h2>
                
                {% assign sorted_tags = site.tags | sort %}
                {% for tag in sorted_tags %}
                <section id="{{ tag[0] | slugify }}" class="tag-section">
                    <h3 class="tag-section-title">
                        {{ tag[0] | replace: '-', ' ' | capitalize }} 
                        <span class="tag-count">({{ tag[1] | size }} articles)</span>
                    </h3>
                    
                    <div class="tag-articles">
                        {% for post in tag[1] %}
                        <div class="tag-article">
                            <a href="{{ post.url | relative_url }}" class="tag-article-link">
                                <span class="article-category">{{ post.category_display | default: post.categories[0] | capitalize }}</span>
                                <span class="article-title">{{ post.title }}</span>
                                <span class="article-date">{{ post.date | date: "%b %d, %Y" }}</span>
                            </a>
                        </div>
                        {% endfor %}
                    </div>
                </section>
                {% endfor %}
            </div>
        </section>
    </div>
    
    <aside class="author-bio-sidebar">
        <div class="stats-section">
            <h3>Topic Statistics</h3>
            <div class="stats-grid">
                <div class="stat-item">
                    <div class="stat-number">{{ site.tags | size }}</div>
                    <div class="stat-label">Total Topics</div>
                </div>
                <div class="stat-item">
                    <div class="stat-number">{{ site.posts | size }}</div>
                    <div class="stat-label">Total Articles</div>
                </div>
            </div>
        </div>
        
        <div class="top-tags-section">
            <h3>Most Active Topics</h3>
            {% assign top_tags = site.tags | sort: 'size' | reverse %}
            {% for tag in top_tags limit:8 %}
            <a href="#{{ tag[0] | slugify }}" class="top-tag-link">
                <span>{{ tag[0] | replace: '-', ' ' | capitalize }}</span>
                <span class="top-tag-count">{{ tag[1] | size }}</span>
            </a>
            {% endfor %}
        </div>
    </aside>
</div>
