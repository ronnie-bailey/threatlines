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
                <div id="{{ tag[0] | slugify }}" class="featured-card" style="margin-bottom: 2rem; padding: 0;">
                    <div class="featured-content">
                        <h3 class="featured-title" style="color: #00d4ff; border-bottom: 2px solid #00d4ff; padding-bottom: 0.5rem;">
                            {{ tag[0] | replace: '-', ' ' | capitalize }} ({{ tag[1] | size }} articles)
                        </h3>
                        
                        {% for post in tag[1] %}
                        <div style="padding: 0.75rem 0; border-bottom: 1px solid rgba(0, 212, 255, 0.1);">
                            <a href="{{ post.url | relative_url }}" style="text-decoration: none; display: flex; justify-content: space-between; align-items: center; gap: 1rem;">
                                <div style="flex: 1;">
                                    <span style="color: #1db584; font-size: 0.8rem; text-transform: uppercase; font-weight: 600; display: block;">{{ post.category_display | default: post.categories[0] | capitalize }}</span>
                                    <span style="color: #e2e8f0; font-weight: 500; line-height: 1.4;">{{ post.title }}</span>
                                </div>
                                <span style="color: #a0aec0; font-size: 0.9rem; min-width: 80px; text-align: right;">{{ post.date | date: "%b %Y" }}</span>
                            </a>
                        </div>
                        {% endfor %}
                    </div>
                </div>
                {% endfor %}
            </div>
        </section>
    </div>
    
    <aside class="author-bio-sidebar">
        <div style="text-align: center; margin-bottom: 2rem; padding-bottom: 2rem; border-bottom: 1px solid var(--border-subtle);">
            <h3 style="color: #00d4ff; margin-bottom: 1rem;">Topic Statistics</h3>
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; text-align: center;">
                <div style="background: rgba(0, 212, 255, 0.1); padding: 1rem; border-radius: 8px;">
                    <div style="font-size: 1.5rem; font-weight: 700; color: #00d4ff;">{{ site.tags | size }}</div>
                    <div style="font-size: 0.8rem; color: #a0aec0;">Topics</div>
                </div>
                <div style="background: rgba(0, 212, 255, 0.1); padding: 1rem; border-radius: 8px;">
                    <div style="font-size: 1.5rem; font-weight: 700; color: #00d4ff;">{{ site.posts | size }}</div>
                    <div style="font-size: 0.8rem; color: #a0aec0;">Articles</div>
                </div>
            </div>
        </div>
    </aside>
</div>
