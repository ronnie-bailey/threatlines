---
layout: default
title: All Topics & Tags
permalink: /tags/
---

<!-- Force clear any existing content -->
<style>
/* Force override any existing tag page styles */
body .page-content * {
    background: transparent !important;
}
</style>

<div class="main-container">
    <div class="left-column">
        <section class="tag-cloud-section">
            <h2>🏷️ Browse All Topics</h2>
            
            <!-- NEW: Tag Overview Grid -->
            <div class="tag-cloud" style="margin-bottom: 3rem;">
                <h3 style="color: #00d4ff; margin-bottom: 1rem; font-family: var(--font-mono);">Most Popular</h3>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 1rem;">
                    {% assign sorted_tags = site.tags | sort: 'size' | reverse %}
                    {% for tag in sorted_tags limit:12 %}
                    <a href="#{{ tag[0] | slugify }}" style="
                        background: rgba(0, 212, 255, 0.1) !important;
                        border: 1px solid rgba(0, 212, 255, 0.2) !important;
                        border-radius: 8px !important;
                        padding: 1rem !important;
                        text-decoration: none !important;
                        display: flex !important;
                        justify-content: space-between !important;
                        align-items: center !important;
                        transition: all 0.3s ease !important;
                        font-family: var(--font-mono) !important;
                    ">
                        <span style="color: #e2e8f0 !important; font-weight: 500 !important;">
                            {{ tag[0] | replace: '-', ' ' | capitalize }}
                        </span>
                        <span style="
                            background: #00d4ff !important;
                            color: #0f1419 !important;
                            padding: 0.25rem 0.5rem !important;
                            border-radius: 12px !important;
                            font-size: 0.8rem !important;
                            font-weight: 600 !important;
                        ">{{ tag[1].size }}</span>
                    </a>
                    {% endfor %}
                </div>
            </div>
            
            <!-- NEW: Organized by First Letter -->
            <div style="margin-top: 3rem;">
                <h2>📡 All Topics A-Z</h2>
                
                {% assign sorted_tags = site.tags | sort %}
                {% assign current_letter = '' %}
                
                {% for tag in sorted_tags %}
                {% assign first_letter = tag[0] | slice: 0 | upcase %}
                
                {% if first_letter != current_letter %}
                    {% unless forloop.first %}</div></div>{% endunless %}
                    {% assign current_letter = first_letter %}
                    
                    <div style="
                        background: rgba(29, 181, 132, 0.05) !important;
                        border-radius: 12px !important;
                        padding: 1.5rem !important;
                        border-left: 4px solid #1db584 !important;
                        margin-bottom: 2rem !important;
                    ">
                        <h3 style="
                            color: #1db584 !important;
                            font-size: 1.5rem !important;
                            font-weight: 700 !important;
                            margin-bottom: 1rem !important;
                            font-family: var(--font-mono) !important;
                        ">{{ current_letter }}</h3>
                        <div style="display: grid; gap: 1rem;">
                {% endif %}
                
                <div id="{{ tag[0] | slugify }}" style="
                    background: rgba(0, 212, 255, 0.05) !important;
                    border-radius: 8px !important;
                    padding: 1rem !important;
                    border: 1px solid rgba(0, 212, 255, 0.1) !important;
                ">
                    <h4 style="
                        color: #00d4ff !important;
                        margin: 0 0 1rem 0 !important;
                        font-family: var(--font-mono) !important;
                        display: flex !important;
                        align-items: center !important;
                        gap: 0.5rem !important;
                    ">
                        <span style="color: #1db584 !important;">#</span>
                        {{ tag[0] | replace: '-', ' ' | capitalize }}
                        <span style="
                            background: rgba(0, 212, 255, 0.2) !important;
                            color: #00d4ff !important;
                            padding: 0.2rem 0.5rem !important;
                            border-radius: 10px !important;
                            font-size: 0.7rem !important;
                            margin-left: auto !important;
                        ">{{ tag[1].size }} articles</span>
                    </h4>
                    
                    <div style="display: flex; flex-direction: column; gap: 0.5rem;">
                        {% for post in tag[1] limit:3 %}
                        <div style="
                            padding: 0.5rem !important;
                            background: rgba(0, 212, 255, 0.03) !important;
                            border-radius: 4px !important;
                            border-left: 2px solid rgba(0, 212, 255, 0.3) !important;
                        ">
                            <a href="{{ post.url | relative_url }}" style="
                                display: flex !important;
                                justify-content: space-between !important;
                                align-items: center !important;
                                text-decoration: none !important;
                                gap: 1rem !important;
                            ">
                                <span style="
                                    color: #1db584 !important;
                                    font-size: 0.7rem !important;
                                    text-transform: uppercase !important;
                                    font-weight: 600 !important;
                                    font-family: var(--font-mono) !important;
                                    min-width: 80px !important;
                                ">{{ post.category_display | default: post.categories[0] | capitalize }}</span>
                                
                                <span style="
                                    color: #e2e8f0 !important;
                                    font-size: 0.9rem !important;
                                    flex: 1 !important;
                                    font-weight: 500 !important;
                                ">{{ post.title }}</span>
                                
                                <span style="
                                    color: #a0aec0 !important;
                                    font-size: 0.8rem !important;
                                    font-family: var(--font-mono) !important;
                                    min-width: 60px !important;
                                    text-align: right !important;
                                ">{{ post.date | date: "%b %Y" }}</span>
                            </a>
                        </div>
                        {% endfor %}
                        
                        {% if tag[1].size > 3 %}
                        <div style="
                            text-align: center !important;
                            padding: 0.5rem !important;
                            font-style: italic !important;
                            color: #a0aec0 !important;
                            font-size: 0.8rem !important;
                        ">+{{ tag[1].size | minus: 3 }} more articles</div>
                        {% endif %}
                    </div>
                </div>
                
                {% if forloop.last %}</div></div>{% endif %}
                {% endfor %}
            </div>
        </section>
    </div>
    
    <!-- Right Column - Enhanced Navigation -->
    <aside class="author-bio-sidebar">
        <div style="margin-bottom: 2rem; padding-bottom: 2rem; border-bottom: 1px solid var(--border-subtle);">
            <h3 style="color: #00d4ff !important; margin-bottom: 1rem !important; font-family: var(--font-mono) !important;">Quick Jump</h3>
            <div style="
                display: grid !important;
                grid-template-columns: repeat(6, 1fr) !important;
                gap: 0.25rem !important;
            ">
                {% assign letters = 'A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z' | split: ',' %}
                {% for letter in letters %}
                <a href="#section-{{ letter }}" style="
                    background: rgba(0, 212, 255, 0.1) !important;
                    color: #00d4ff !important;
                    text-decoration: none !important;
                    padding: 0.5rem !important;
                    text-align: center !important;
                    border-radius: 4px !important;
                    font-family: var(--font-mono) !important;
                    font-size: 0.8rem !important;
                    transition: all 0.3s ease !important;
                ">{{ letter }}</a>
                {% endfor %}
            </div>
        </div>
        
        <div style="margin-bottom: 2rem;">
            <h3 style="color: #00d4ff !important; margin-bottom: 1rem !important; font-family: var(--font-mono) !important;">Stats</h3>
            <div style="
                display: grid !important;
                grid-template-columns: 1fr 1fr !important;
                gap: 1rem !important;
                text-align: center !important;
            ">
                <div style="
                    background: rgba(0, 212, 255, 0.1) !important;
                    padding: 1rem !important;
                    border-radius: 8px !important;
                ">
                    <div style="
                        font-size: 1.5rem !important;
                        font-weight: 700 !important;
                        color: #00d4ff !important;
                        font-family: var(--font-mono) !important;
                    ">{{ site.tags | size }}</div>
                    <div style="
                        font-size: 0.8rem !important;
                        color: #a0aec0 !important;
                        margin-top: 0.25rem !important;
                    ">Topics</div>
                </div>
                <div style="
                    background: rgba(0, 212, 255, 0.1) !important;
                    padding: 1rem !important;
                    border-radius: 8px !important;
                ">
                    <div style="
                        font-size: 1.5rem !important;
                        font-weight: 700 !important;
                        color: #00d4ff !important;
                        font-family: var(--font-mono) !important;
                    ">{{ site.posts | size }}</div>
                    <div style="
                        font-size: 0.8rem !important;
                        color: #a0aec0 !important;
                        margin-top: 0.25rem !important;
                    ">Articles</div>
                </div>
            </div>
        </div>
        
        <div>
            <h3 style="color: #00d4ff !important; margin-bottom: 1rem !important; font-family: var(--font-mono) !important;">Top Topics</h3>
            {% assign top_tags = site.tags | sort: 'size' | reverse %}
            <div style="
                display: flex !important;
                flex-direction: column !important;
                gap: 0.5rem !important;
            ">
                {% for tag in top_tags limit:8 %}
                <a href="#{{ tag[0] | slugify }}" style="
                    display: flex !important;
                    justify-content: space-between !important;
                    padding: 0.5rem !important;
                    background: rgba(0, 212, 255, 0.05) !important;
                    border-radius: 6px !important;
                    text-decoration: none !important;
                    transition: all 0.3s ease !important;
                ">
                    <span style="
                        color: #e2e8f0 !important;
                        font-size: 0.9rem !important;
                    ">{{ tag[0] | replace: '-', ' ' | capitalize }}</span>
                    <span style="
                        background: #1db584 !important;
                        color: #0f1419 !important;
                        padding: 0.2rem 0.5rem !important;
                        border-radius: 10px !important;
                        font-size: 0.7rem !important;
                        font-weight: 600 !important;
                    ">{{ tag[1] | size }}</span>
                </a>
                {% endfor %}
            </div>
        </div>
    </aside>
</div>
