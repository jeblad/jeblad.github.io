---
layout: page
title: Projects
permalink: /projects/
header: Collection of documentation for various projects, not only for artificial neural nets.
group: navigation
weight: 98
category: pages
tags: [repo]
use_math: exclude
---

This is a collection of documentation for various projects, not only for artificial neural nets, but for code and libraries the author(s) find interesting or has invested time into. Usually there should be one or more links to the library itself, and one or more links to the documentation.

For further information, check the page for each project.

## Projects

<ul class="leading">
{% for project in site.projects %}
<li><a href="{{ project.url }}">{{ project.title }}</a>{% if project.tagline %} – {{ project.tagline }}{% endif %}</li>
{% endfor %}
</ul>