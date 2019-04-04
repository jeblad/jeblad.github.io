---
layout: page
title: About
permalink: /about/
use_math: exclude
---

This site is devoted to various topics that the author(s) find interesting. Most of the articles should be fairly easy reading, while the more lengthy articles might be more demanding. The various articles should have a byline where at least the main author is listed.

For further information, check the page for individual authors.

## Authors

<ul class="leading">
{% for author in site.authors %}
<li><a href="{{ author.url }}">{{ author.name }}</a>{% if author.tagline %} – {{ author.tagline }}{% endif %}</li>
{% endfor %}
</ul>
