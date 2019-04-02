---
layout: page
title: About
permalink: /about/
---

<h2>Site</h2>

This site is devoted to various topics that the author(s) find interesting. Most of the articles should be fairly easy reading, while the more lengthy articles might be more demanding. The various articles should have a byline where at least the main author is listed.

<h2>Authors</h2>
{% for author in site.authors %}
  <h3>{{ author[1].name }}</h3>
  <table class="identities">
    {% if author[1].email %}
    <tr><th>Email:</th><td><a href="mailto:{{author[1].email}}">{{ author[1].email }}</a></td></tr>
    {% endif %}
    {% if author[1].github %}
    <tr><th>Github</th><td><a href="https://github.com/{{author[1].github}}">{{ author[1].github }}</a></td></tr>
    {% endif %}
    {% if author[1].twitter %}
    <tr><th>Twitter</th><td><a href="https://twitter.com/{{author[1].twitter}}">@{{ author[1].twitter }}</a></td></tr>
    {% endif %}
    {% if author[1].keybase %}
    <tr><th>Keybase</th><td><a href="https://keybase.io/{{author[1].keybase}}">{{ author[1].keybase }}</a></td></tr>
    {% endif %}
    {% if author[1].linkedin %}
    <tr><th>Linkedin</th><td><a href="https://www.linkedin.com/in/{{author[1].wikimedia}}">{{ author[1].linkedin }}</a></td></tr>
    {% endif %}
    {% if author[1].wikimedia %}
    <tr><th>Wikimedia</th><td><a href="https://meta.wikimedia.org/wiki/user:{{author[1].wikimedia}}">User:{{ author[1].wikimedia }}</a></td></tr>
    {% endif %}
  </table>

  {% if author[1].github %}
  {% avatar {{ author[1].github }} %}
  {% endif %}

  {% if author[1].about %}
  {{ author[1].about }}
  {% endif %}

{% endfor %}
