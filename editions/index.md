---
layout: default
title: Archived editions
permalink: /editions/
---

# Archived editions

{% assign pdfs = site.static_files | where_exp: "f", "f.path contains '/editions/' and f.extname == '.pdf'" %}
{% assign groups = pdfs | group_by_exp: "f", "f.path | split: '/' | slice: 2,1 | first" %}
{% assign groups = groups | sort: "name" | reverse %}

{% if groups == empty %}
_No editions have been published yet._
{% else %}
{% for g in groups %}
## Edition {{ g.name }}
<ul>
  {% assign files = g.items | sort: "path" %}
  {% for f in files %}
  <li><a href="{{ f.path | relative_url }}">{{ f.name }}</a></li>
  {% endfor %}
</ul>
{% endfor %}
{% endif %}
