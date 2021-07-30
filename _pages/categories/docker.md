---
layout: archive
permalink: /docker/
title: "Docker"

author_profile: true
sidebar:
  nav: "docs"
---

{% assign posts = site.categories.docker %}
{% for post in posts %}
  {% include custom-archive-single.html type=entries_layout %}
{% endfor %}