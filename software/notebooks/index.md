---
layout: page
title: Notebooks & Codes
subtitle: Browse our Python Jupyter Notebooks
---

Welcome to our Notebooks gallery. Here group members have provided interactive codes covering a variety of fields. Choose a notebook below to see the python code and explanations.

<div class="row">
  {% assign all_notebooks = site.notebooks | sort: "order" %}
  {% for nb in all_notebooks %}
  <div class="col-md-12 mb-4">
    <div class="card flex-row" style="border: 1px solid #ddd; border-radius: 8px; overflow: hidden; padding: 15px;">
      <div class="card-body">
        <h3 style="margin-top: 0;"><a href="{{ nb.url | relative_url }}">{{ nb.title }}</a></h3>
        <p style="color: #666; font-size: 0.9em; margin-bottom: 5px;">Topic: <strong>{{ nb.topic }}</strong></p>
        <p>{{ nb.tldr }}</p>
        <a href="{{ nb.url | relative_url }}" class="btn btn-outline-primary btn-sm">View Notebook</a>
      </div>
    </div>
  </div>

  <div class="col-md-12 mb-4">
    <div class="card flex-row" style="border: 1px solid #ddd; border-radius: 8px; overflow: hidden; padding: 15px;">
      <div class="card-body">
        <h3 style="margin-top: 0;"><a href="{{ '/software/applications/2026-accelerate-cfd' | relative_url }}">{{ Acclerate CFD }}</a></h3>
        <p style="color: #666; font-size: 0.9em; margin-bottom: 5px;">Topic: <strong>{{ Accelerate CFD }}</strong></p>
        <p>{{ nb.tldr }}</p>
        <a href="{{ '/software/applications/2026-accelerate-cfd' | relative_url }}" class="btn btn-outline-primary btn-sm">View Notebook</a>
      </div>
    </div>
  </div>
  {% endfor %}

</div>
