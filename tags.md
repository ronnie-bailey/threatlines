---
layout: default
title: Popular Topics
permalink: /tags/
---

<div class="main-container">
    <div class="left-column">
        <section class="tag-cloud-section">
            <h2>🏷️ Browse by Topic</h2>
            
            <!-- Tag Cloud Overview -->
            <div class="tag-cloud">
                <div class="tag-overview-grid">
                    {% assign sorted_tags = site.tags | sort: 'size' | reverse %}
                    {% for tag in sorted_tags limit:20 %}
                    {% assign tag_size_class = 'tag-size-1' %}
                    {% if tag[1].size >= 5 %}
                        {% assign tag_size_class = 'tag-size-4' %}
                    {% elsif tag[1].size >= 3 %}
                        {% assign tag_size_class = 'tag-size-3' %}
                    {% elsif tag[1].size >= 2 %}
                        {% assign tag_size_class = 'tag-size-2' %}
                    {% endif %}
                    
                    <a href="#{{ tag[0] | slugify }}" class="tag-overview-item {{ tag_size_class }}">
                        <span class="tag-name">{{ tag[0] | replace: '-', ' ' | capitalize }}</span>
                        <span class="tag-count">{{ tag[1].size }}</span>
                    </a>
                    {% endfor %}
                </div>
            </div>
            
            <!-- Organized Tag Sections -->
            <div class="tags-by-category">
                <h2>📡 All Topics</h2>
                
                {% assign sorted_tags = site.tags | sort %}
                {% assign current_letter = '' %}
                
                <div class="tag-sections">
                    {% for tag in sorted_tags %}
                    {% assign first_letter = tag[0] | slice: 0 | upcase %}
                    
                    {% if first_letter != current_letter %}
                        {% unless forloop.first %}</div>{% endunless %}
                        {% assign current_letter = first_letter %}
                        
                        <div class="tag-section" id="section-{{ current_letter }}">
                            <h3 class="section-letter">{{ current_letter }}</h3>
                            <div class="tag-section-content">
                    {% endif %}
                    
                    <div class="tag-entry" id="{{ tag[0] | slugify }}">
                        <div class="tag-header">
                            <h4 class="tag-title">
                                <span class="tag-icon">#</span>
                                {{ tag[0] | replace: '-', ' ' | capitalize }}
                                <span class="tag-badge">{{ tag[1].size }} articles</span>
                            </h4>
                        </div>
                        
                        <div class="tag-articles">
                            {% for post in tag[1] limit:3 %}
                            <div class="tag-article-item">
                                <a href="{{ post.url | relative_url }}" class="tag-article-link">
                                    <span class="article-category">{{ post.category_display | default: post.categories[0] | capitalize }}</span>
                                    <span class="article-title">{{ post.title }}</span>
                                    <span class="article-date">{{ post.date | date: "%b %Y" }}</span>
                                </a>
                            </div>
                            {% endfor %}
                            
                            {% if tag[1].size > 3 %}
                            <div class="show-more">
                                <span class="more-count">+{{ tag[1].size | minus: 3 }} more articles</span>
                            </div>
                            {% endif %}
                        </div>
                    </div>
                    
                    {% if forloop.last %}</div></div>{% endif %}
                    {% endfor %}
                </div>
            </div>
        </section>
    </div>
    
    <!-- Right Column - Navigation & Stats -->
    <aside class="author-bio-sidebar">
        <div style="margin-bottom: 2rem; padding-bottom: 2rem; border-bottom: 1px solid var(--border-subtle);">
            <h3 style="color: #00d4ff; margin-bottom: 1rem; font-family: var(--font-mono);">Quick Navigation</h3>
            <div class="alphabet-nav">
                {% assign letters = 'A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z' | split: ',' %}
                {% for letter in letters %}
                <a href="#section-{{ letter }}" class="nav-letter">{{ letter }}</a>
                {% endfor %}
            </div>
        </div>
        
        <div style="margin-bottom: 2rem;">
            <h3 style="color: #00d4ff; margin-bottom: 1rem; font-family: var(--font-mono);">Topic Stats</h3>
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
        
        <div>
            <h3 style="color: #00d4ff; margin-bottom: 1rem; font-family: var(--font-mono);">Most Active</h3>
            {% assign top_tags = site.tags | sort: 'size' | reverse %}
            <div class="top-tags-list">
                {% for tag in top_tags limit:8 %}
                <a href="#{{ tag[0] | slugify }}" class="top-tag-item">
                    <span class="top-tag-name">{{ tag[0] | replace: '-', ' ' | capitalize }}</span>
                    <span class="top-tag-count">{{ tag[1].size }}</span>
                </a>
                {% endfor %}
            </div>
        </div>
    </aside>
</div>

<style>
/* Tag Overview Grid */
.tag-overview-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
    margin-bottom: 3rem;
}

.tag-overview-item {
    background: rgba(0, 212, 255, 0.1);
    border: 1px solid rgba(0, 212, 255, 0.2);
    border-radius: 8px;
    padding: 1rem;
    text-decoration: none;
    display: flex;
    justify-content: space-between;
    align-items: center;
    transition: all 0.3s ease;
    font-family: var(--font-mono);
}

.tag-overview-item:hover {
    background: rgba(0, 212, 255, 0.2);
    transform: translateY(-2px);
    border-color: #00d4ff;
}

.tag-name {
    color: #e2e8f0;
    font-weight: 500;
}

.tag-count {
    background: #00d4ff;
    color: #0f1419;
    padding: 0.25rem 0.5rem;
    border-radius: 12px;
    font-size: 0.8rem;
    font-weight: 600;
}

/* Alphabetical Sections */
.tag-sections {
    display: flex;
    flex-direction: column;
    gap: 2rem;
}

.tag-section {
    background: rgba(29, 181, 132, 0.05);
    border-radius: 12px;
    padding: 1.5rem;
    border-left: 4px solid #1db584;
}

.section-letter {
    color: #1db584;
    font-size: 1.5rem;
    font-weight: 700;
    margin-bottom: 1rem;
    font-family: var(--font-mono);
}

.tag-section-content {
    display: grid;
    gap: 1.5rem;
}

.tag-entry {
    background: rgba(0, 212, 255, 0.05);
    border-radius: 8px;
    padding: 1rem;
    border: 1px solid rgba(0, 212, 255, 0.1);
}

.tag-header {
    margin-bottom: 1rem;
}

.tag-title {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    font-size: 1.1rem;
    color: #00d4ff;
    margin: 0;
    font-family: var(--font-mono);
}

.tag-icon {
    color: #1db584;
    font-weight: 700;
}

.tag-badge {
    background: rgba(0, 212, 255, 0.2);
    color: #00d4ff;
    padding: 0.2rem 0.5rem;
    border-radius: 10px;
    font-size: 0.7rem;
    margin-left: auto;
}

.tag-articles {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.tag-article-item {
    padding: 0.5rem;
    background: rgba(0, 212, 255, 0.03);
    border-radius: 4px;
    border-left: 2px solid rgba(0, 212, 255, 0.3);
}

.tag-article-link {
    display: flex;
    justify-content: space-between;
    align-items: center;
    text-decoration: none;
    gap: 1rem;
}

.article-category {
    color: #1db584;
    font-size: 0.7rem;
    text-transform: uppercase;
    font-weight: 600;
    font-family: var(--font-mono);
    min-width: 80px;
}

.article-title {
    color: #e2e8f0;
    font-size: 0.9rem;
    flex: 1;
    font-weight: 500;
}

.article-date {
    color: #a0aec0;
    font-size: 0.8rem;
    font-family: var(--font-mono);
    min-width: 60px;
    text-align: right;
}

.tag-article-link:hover .article-title {
    color: #00d4ff;
}

.show-more {
    text-align: center;
    padding: 0.5rem;
    font-style: italic;
    color: #a0aec0;
    font-size: 0.8rem;
}

/* Sidebar Navigation */
.alphabet-nav {
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    gap: 0.25rem;
}

.nav-letter {
    background: rgba(0, 212, 255, 0.1);
    color: #00d4ff;
    text-decoration: none;
    padding: 0.5rem;
    text-align: center;
    border-radius: 4px;
    font-family: var(--font-mono);
    font-size: 0.8rem;
    transition: all 0.3s ease;
}

.nav-letter:hover {
    background: rgba(0, 212, 255, 0.2);
    transform: scale(1.1);
}

.stats-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
    text-align: center;
}

.stat-item {
    background: rgba(0, 212, 255, 0.1);
    padding: 1rem;
    border-radius: 8px;
}

.stat-number {
    font-size: 1.5rem;
    font-weight: 700;
    color: #00d4ff;
    font-family: var(--font-mono);
}

.stat-label {
    font-size: 0.8rem;
    color: #a0aec0;
    margin-top: 0.25rem;
}

.top-tags-list {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.top-tag-item {
    display: flex;
    justify-content: space-between;
    padding: 0.5rem;
    background: rgba(0, 212, 255, 0.05);
    border-radius: 6px;
    text-decoration: none;
    transition: all 0.3s ease;
}

.top-tag-item:hover {
    background: rgba(0, 212, 255, 0.1);
}

.top-tag-name {
    color: #e2e8f0;
    font-size: 0.9rem;
}

.top-tag-count {
    background: #1db584;
    color: #0f1419;
    padding: 0.2rem 0.5rem;
    border-radius: 10px;
    font-size: 0.7rem;
    font-weight: 600;
}

@media (max-width: 768px) {
    .tag-overview-grid {
        grid-template-columns: 1fr;
    }
    
    .alphabet-nav {
        grid-template-columns: repeat(4, 1fr);
    }
    
    .tag-article-link {
        flex-direction: column;
        align-items: flex-start;
        gap: 0.25rem;
    }
    
    .article-date {
        text-align: left;
        min-width: auto;
    }
}
</style>
