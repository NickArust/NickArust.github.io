---
layout: default
title: "Personal Projects"
description: "A collection of my personal coding projects in Scientific Computing and ML."
permalink: /projects/
---

<h1>Personal Projects</h1>

<div class="project-grid">
  {% assign projects = site.pages | sort: 'date' | reverse %}
  {% for project in projects %}
    {% if project.url contains '/personal_projects/' and project.title %}
      <div class="project-card">
        
        {% if project.image %}
          <img src="{{ project.image | relative_url }}" alt="{{ project.title }}">
        {% endif %}

        <div class="project-content">
          <h3><a href="{{ project.url | relative_url }}">{{ project.title }}</a></h3>
          
          <p>{{ project.excerpt | default: "View project details" | strip_html | truncate: 120 }}</p>
          
          {% if project.skills %}
            <div class="tech-stack" style="margin-top: 0.5rem;">
              {% for skill in project.skills %}
                <span class="tech-badge">{{ skill }}</span>
              {% endfor %}
            </div>
          {% endif %}
          
          <a href="{{ project.url | relative_url }}" class="btn" style="margin-top: 1rem; padding: 0.5rem 1rem; font-size: 0.9rem;">Read More</a>
        </div>
      </div>
    {% endif %}
  {% endfor %}
</div>