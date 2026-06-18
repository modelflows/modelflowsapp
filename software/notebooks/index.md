---
layout: page
title: Notebooks & Codes
subtitle: Explore Interactive Tutorials and Python Implementations
---

Welcome to our collection of Jupyter notebooks, research codes, and reference implementations. These resources provide practical examples of ModelFLOWs methodologies, including modal decomposition, reduced-order modeling, deep learning, forecasting, data assimilation, and CFD applications. Select a resource below to explore the code, methodology, and results.

<div class="row">
  {% assign all_notebooks = site.notebooks | sort: "order" %}
  {% for nb in all_notebooks %}
  <div class="col-md-6 mb-4">
    <div class="card h-100" style="border: 1px solid #ddd; border-radius: 8px; overflow: hidden;">
      <div class="card-body d-flex flex-column" style="padding: 30px;">
        <h3 style="margin-top: 0; word-break: normal; overflow-wrap: normal;"><a href="{{ nb.url | relative_url }}">{{ nb.title }}</a></h3>
        <p style="color: #666; font-size: 0.9em; margin-bottom: 5px;">Topic: <strong>{{ nb.topic }}</strong></p>
        <p>{{ nb.tldr }}</p>
        <a href="{{ nb.url | relative_url }}"
           class="btn btn-outline-primary btn-sm mt-auto align-self-start">
          View Notebook</a>
      </div>
    </div>
  </div>
  {% endfor %}
</div>
