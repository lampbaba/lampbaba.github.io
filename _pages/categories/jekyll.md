---
layout: archive
permalink: /jekyll/
title: "Jekyll"
excerpt: "Jekyll을 이용한 블로그 꾸미기"

# images\wordpress-265132_1920.jpg
author_profile: true
sidebar:
  nav: "docs"

header:
  overlay_image: /images/blog-2355684_1920.jpg
  overlay_filter: 0.5 # 투명도
---

{% assign posts = site.categories.jekyll %}
{% for post in posts %}
  {% include custom-archive-single.html type=entries_layout %}
{% endfor %}