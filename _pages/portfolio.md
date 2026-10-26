---
layout: archive
title: "Current and Recent Projects"
permalink: /portfolio/
author_profile: true
---

{% include base_path %}

<div class="project-grid">
  {% for post in site.portfolio %}
    <article class="project-card">

      {% if post.image %}
        <a href="{{ post.url | relative_url }}" class="project-card__image-link">
          <img
            src="{{ post.image | relative_url }}"
            alt="{{ post.title | escape }}"
            class="project-card__image"
            loading="lazy"
          >
        </a>
      {% endif %}

      <div class="project-card__content">
        <h2 class="project-card__title">
          <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        </h2>

        {% if post.excerpt %}
          <p>{{ post.excerpt | markdownify | remove: '<p>' | remove: '</p>' }}</p>
        {% endif %}

        <a class="project-card__link" href="{{ post.url | relative_url }}">Learn more →</a>
      </div>

    </article>
  {% endfor %}
</div>
