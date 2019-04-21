---
layout: page
title: Authors
permalink: /authors/
use_math: exclude
weight: 980
---

The authors of this small site is listed below. They are not expected to be many, as this is not a collaborative site per see, but an ego trip by [jeblad](/authors/jeblad/). It was also made as an opportunity to check out some new software.

For further information, check the page for individual authors.

## Authors

<ul class="leading">
{% for author in site.authors %}
<li><a href="{{ author.url }}">{{ author.name }}</a>{% if author.tagline %} – {{ author.tagline }}{% endif %}</li>
{% endfor %}
</ul>
