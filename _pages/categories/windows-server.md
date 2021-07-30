---
layout: archive
permalink: /windows-server/
title: "Windows Server"

author_profile: true
sidebar:
  nav: "docs"
---

{% assign posts = site.categories.windows-server %}
{% for post in posts %}
  {% include custom-archive-single.html type=entries_layout %}
{% endfor %}