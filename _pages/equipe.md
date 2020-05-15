---
title: Equipe
tagline: Confira quem faz parte do Buteco
layout: page
permalink: equipe
toc: true
header:
  overlay_color: "#333"
  show_overlay_excerpt: true
---

## Administradores

Pessoas que são responsáveis por manter o site no ar e atualizado.

{% for username in site.data.team.maintainers %}
  {% assign user = site.data.authors[username] %}
  {% include user-profile.html %}
{% endfor %}

## Colaboradores

Pessoas que colaboram com artigos regularmente ou que já fizeram parte da equipe do Buteco no passado.

{% for username in site.data.team.collaborators %}
  {% assign user = site.data.authors[username] %}
  {% include user-profile.html %}
{% endfor %}
