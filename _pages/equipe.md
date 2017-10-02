---
title: Equipe
layout: page
permalink: /equipe/
author_profile: false
comments: false
related: false
share: false
---

{% include base_path %}

{% for username in site.data.authors.active_authors %}
  {% assign author=site.data.authors[username] %}
  {% include author-profile.html %}
{% endfor %}
