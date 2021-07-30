---
layout: archive
permalink: /csharp/
title: "C#"

author_profile: true
sidebar:
  nav: "docs"
---

{% assign posts = site.categories.csharp %}
{% for post in posts %}
  {% include custom-archive-single.html type=entries_layout %}
{% endfor %}