---
layout: page
title: Blog
redirect_from: "/"
---

{% for post in site.posts %}
  {{ post.date | date_to_string }} - [ {{ post.title }} ]({{ post.url }})
{% endfor %}
