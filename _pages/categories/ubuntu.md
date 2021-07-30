---
layout: archive
permalink: /ubuntu/
title: "Ubuntu"

author_profile: true
sidebar:
  nav: "docs"
---

{% assign posts = site.categories.ubuntu %}
{% for post in posts %}
  {% include custom-archive-single.html type=entries_layout %}
{% endfor %}