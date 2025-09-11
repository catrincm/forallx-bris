---
layout: default
title: Archived editions

---

# Archived editions

{% assign files = site.static_files | where: "extname", ".pdf" | sort: "path" %}

{% assign current_year = "" %}
{% for f in files %}
  {% if f.path contains "/editions/" %}
    {% assign parts = f.path | split: "/" %}
    {% assign year = parts[2] %}
    {% if year != current_year %}
## {{ year }}
{% assign current_year = year %}
    {% endif %}
- <a href="{{ f.path | relative_url }}">{{ f.name }}</a>
  {% endif %}
{% endfor %}
