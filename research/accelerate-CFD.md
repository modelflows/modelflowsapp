---
layout: page
title: Accelerate CFD
subtitle: Frameworks and surrogate methodologies for accelerating CFD simulations
---

This section collects research posts related to CFD acceleration, adaptive prediction, surrogate modelling, reduced-order modelling, and data-driven workflows for high-fidelity simulations.



<div class="row">
  {% assign adaptive_posts = site.research | where: "topic", "Adaptive prediction" %}
  {% for post in adaptive_posts %}
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
        <a href="{{ _research/cfd-simulations/Accelerate CFD/Adaptive_prediction.md | relative_url }}" class="btn btn-outline-primary btn-sm">Read More</a>
      </div>
    </div>
  </div>
  {% endfor %}
</div>



<div class="row">
  {% assign rans_posts = site.research | where: "topic", "RANS acceleration" %}
  {% for post in rans_posts %}
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
