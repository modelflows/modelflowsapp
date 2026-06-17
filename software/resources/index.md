---
layout: page
title: Resources & Databases
subtitle: Datasets, meshes, CFD cases, simulation outputs and reusable files
---

Welcome to the ModelFLOWs Resources Hub.

{% assign resources = site.resources | sort: "application" %}

<div class="row mt-4">
{% for resource in resources %}
  <div class="col-md-4 mb-4">
    <div class="card h-100 shadow-sm">
      <div class="card-body">
        <h3 class="card-title">{{ resource.title }}</h3>
        <p class="text-muted"><strong>Application:</strong> {{ resource.application }}</p>
        <p class="text-muted"><strong>Type:</strong> {{ resource.resource_type }}</p>
        <p>{{ resource.tldr }}</p>
        <a href="{{ resource.url | relative_url }}" class="btn btn-primary d-block">Open Resource</a>
      </div>
    </div>
  </div>
{% endfor %}
</div>
