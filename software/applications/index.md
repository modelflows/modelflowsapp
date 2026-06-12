---
layout: page
title: Applications
subtitle: End-to-end tutorials, workflows, notebooks, videos, and simulation resources
---

Welcome to the ModelFLOWs Applications Hub. Here you can find complete workflows organized by application area.

{% assign all_apps = site.applications %}
{% for app in all_apps %}

### [{{ app.title }}]({{ app.url | relative_url }})

Area: {{ app.area }}

{{ app.tldr }}

[View Application]({{ app.url | relative_url }})

---

{% endfor %}
