---
layout: page
title: Combustion
subtitle: Analysis of complex reactive flows and thermal dynamics
---

This section collects all the research done by our group regarding combustion simulations and hybrid reduced-order models.

<div class="row">
  {% assign current_posts = site.research | where: "topic", "Combustion" %}
  {% for post in current_posts %}
  <div class="col-md-12 mb-4">
    <div class="card flex-row" style="border: 1px solid #ddd; border-radius: 8px; overflow: hidden; padding: 15px;">
      <div class="card-body">
        <h3 style="margin-top: 0;"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
        <p style="color: #666; font-size: 0.9em; margin-bottom: 5px;">Category: <strong>{{ post.category }}</strong></p>
        <p>{{ post.tldr }}</p>
        {% if post.thumbnail %}
        <img src="{{ post.thumbnail | relative_url }}" style="max-width: 250px; height: auto; margin-top: 10px; margin-bottom: 10px; border-radius: 5px;" alt="Miniature">
        {% endif %}
        <br>
        <a href="{{ post.url | relative_url }}" class="btn btn-outline-primary btn-sm">Read More</a>
      </div>
    </div>
  </div>
  {% endfor %}
</div>
