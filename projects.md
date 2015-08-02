---
layout: page
title: Projects
---

{% for project in site.projects %}

### {{ project.title }}

{{ project.content }}

{% endfor %}
