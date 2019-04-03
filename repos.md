---
layout: page
title: Repos
permalink: /repos/
header: Collection of documentation for various repositories, not only for artificial neural nets.
group: navigation
weight: 98
category: pages
tags: [repo]
---
{_% include JB/setup %_}

<ul class="posts">
  {% for repo in site.repos %}
    {% assign data = repo[1] %}
    <li>{% if data.repo-url %}<a href="{{ data.repo-url | default: repo[0] }}"><strong>{{ repo[0] }}</strong></a>{% else %}<strong>{{ repo[0] }}</strong>{% endif %} {% if data.doc-url %}(<a href="{{ BASE_PATH }}/{{ data.doc-url }}">doc</a>){% endif %} – {{data.description}}</li>
  {% endfor %}
</ul>
