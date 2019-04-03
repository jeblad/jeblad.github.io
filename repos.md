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

## Repos

This is a collection of documentation for various repositories, not only for artificial neural nets, but for interesting code and libraries the author(s) find interesting. Usually there should be a link to the library itself, and one link to the documentation.

{% for repo in site.repos %}
{% assign title = repo[0] %}
{% assign data = repo[1] %}

### {{ title }}

  <table class="metadata">
    {% if data.url %}
    <tr><th>Repository:</th><td><a href="{{ data.url }}">{{ title }}</a></td></tr>
    {% endif %}
    {% for doc in data.docs %}
      {% if doc[1].url %}
      <tr><th>Documentation:</th><td><a href="{{ doc[1].url | absolute_url }}">{{ doc[1].title | default: doc[0] }}</a></td></tr>
      {% endif %}
    {% endfor %}
  </table>

{{data.description}}

{% endfor %}
