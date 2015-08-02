---
title: Projects
layout: page
---

test.

{% for project in site.projects %}
  Here's a project:
  {{ project.title }}
  {{ project.excerpt }}
{% endfor %}
