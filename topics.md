---
layout: default
title: Browse Topics
permalink: /topics/
---

<div class="main-container">
    <div class="left-column">
        <section class="tag-cloud-section">
            <h2>Browse All Topics</h2>
            
            <div class="tag-cloud">
                <div class="tag-list">
                    {% for tag in site.tags %}
                    <a href="#{{ tag[0] | slugify }}" class="tag-item tag-size-3">
                        {{ tag[0] | replace: '-', ' ' | capitalize }} ({{ tag[1].size }})
                    </a>
                    {% endfor %}
                </div>
            </div>
            
            <div style="margin-top: 3rem;">
                <h2>Articles by Topic</h2>
                
                {% for tag in site.tags %}
                <div id="{{ tag[0] | slugify }}" class="featured-card" style="margin-bottom: 2rem;">
                    <div class="featured-content">
                        <h3 class="featured-title">
                            {{ tag[0] | replace: '-', ' ' | capitalize }} ({{ tag[1] | size }})
                        </h3>
                        
                        {% for post in tag[1] %}
                        <div style="padding: 0.5rem 0; border-bottom: 1px solid #333;">
                            <a href="{{ post.url | relative_url }}" style="text-decoration: none; color: #e2e8f0;">
                                {{ post.title }}
                            </a>
                            <span style="color: #a0aec0; font-size: 0.9rem; float: right;">
                                {{ post.date | date: "%b %Y" }}
                            </span>
                            <div style="clear: both;"></div>
                        </div>
                        {% endfor %}
                    </div>
                </div>
                {% endfor %}
            </div>
        </section>
    </div>
    
    <aside class="author-bio-sidebar">
        <h3>Topic Statistics</h3>
        <p>Total Topics: {{ site.tags | size }}</p>
        <p>Total Articles: {{ site.posts | size }}</p>
    </aside>
</div>
