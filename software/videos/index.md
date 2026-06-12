---
layout: page
title: Videos
subtitle: Workshop recordings, demos and short tutorials
---

Welcome to the ModelFLOWs Videos Hub.

{% assign videos = site.videos | sort: "application" %}

<div class="row mt-4">
{% for video in videos %}
  <div class="col-md-4 mb-4">
    <div class="card h-100 shadow-sm">
      <div class="card-body">
        <h3 class="card-title">{{ video.title }}</h3>
        <p class="text-muted"><strong>Application:</strong> {{ video.application }}</p>
        <p class="text-muted"><strong>Category:</strong> {{ video.category }}</p>
        <p>{{ video.tldr }}</p>
        <a href="{{ video.url | relative_url }}" class="btn btn-primary d-block">Open Video</a>
      </div>
    </div>
  </div>
{% endfor %}
</div>
