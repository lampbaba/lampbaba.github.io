---
layout: archive
permalink: /go/
title: ""
# excerpt: "Go Language"

author_profile: true
sidebar:
  nav: "docs"

header:
  overlay_image: /images/golang.jpg
  overlay_filter: 0.5 # 투명도
---

{% assign posts = site.categories.go %}
{% for post in posts %}
  {% include custom-archive-single.html type=entries_layout %}
{% endfor %}