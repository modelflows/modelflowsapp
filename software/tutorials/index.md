---
layout: page
title: Tutorials
subtitle: Step-by-step guides for CFD, AI/data-driven models, simulations and post-processing
---

Welcome to the ModelFLOWs Tutorials Hub.

This section contains all tutorials developed within ModelFLOWs.

Tutorials may be:

- Short self-contained tutorials hosted directly on this website.
- Extended tutorials linked to external repositories or Sphinx documentation.
- CFD workflows.
- AI & Data-Driven workflows.
- Post-processing and analysis guides.

Each tutorial should specify:
- Application area.
- Category.
- Author(s).
- Related notebooks, videos, datasets, and repositories.

{% assign tutorials = site.tutorials | sort: "application" %}

<div class="row mt-4">
{% for tutorial in tutorials %}
  <div class="col-md-4 mb-4">
    <div class="card h-100 shadow-sm">
      <div class="card-body">
        <h3 class="card-title">{{ tutorial.title }}</h3>
        <p class="text-muted"><strong>Application:</strong> {{ tutorial.application }}</p>
        <p class="text-muted"><strong>Category:</strong> {{ tutorial.category }}</p>
        <p>{{ tutorial.tldr }}</p>
        <a href="{{ tutorial.url | relative_url }}" class="btn btn-primary d-block">Open Tutorial</a>
      </div>
    </div>
  </div>
{% endfor %}
</div>
