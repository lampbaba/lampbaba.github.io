---
layout: archive
permalink: /oracle/
title: "Oracle"

author_profile: true
sidebar:
  nav: "docs"
---

{% assign posts = site.categories.oracle %}
{% for post in posts %}
  {% include custom-archive-single.html type=entries_layout %}
{% endfor %}