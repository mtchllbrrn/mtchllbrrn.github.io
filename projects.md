---
layout: page
title: Projects
---

{% for project in site.projects %}

### {{ project.title }}

[more info]({{ project.url }}), [github]({{ project.github }})

{{ project.excerpt }}

{% endfor %}
