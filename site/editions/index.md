---
layout: default
title: Archived editions
---

> **Current version:** see the main page at  
> [https://catrincm.github.io/forallx-bris/](https://catrincm.github.io/forallx-bris/)


# Current

{% assign root_files = site.static_files
  | where: "extname", ".pdf"
  | where_exp: "f", "f.path contains '/editions/' == false"
  | where_exp: "f", "f.path | split: '/' | size == 2"
  | sort: "name" %}

{% assign main       = "/forallxbris.pdf" %}
{% assign accessible = "/forallxbris-accessible.pdf" %}
{% assign answers    = "/forallxbris-withanswers.pdf" %}

{%- comment -%} Preferred files first {%- endcomment -%}
{% for f in root_files %}{% if f.path == main %}
- <a href="{{ f.path | relative_url }}">{{ f.name }}</a>
{% endif %}{% endfor %}

{% for f in root_files %}{% if f.path == accessible %}
- <a href="{{ f.path | relative_url }}">{{ f.name }}</a>
{% endif %}{% endfor %}

{%- comment -%} Any other PDFs {%- endcomment -%}
{% for f in root_files %}
  {% if f.path != main and f.path != accessible and f.path != answers %}
- <a href="{{ f.path | relative_url }}">{{ f.name }}</a>
  {% endif %}
{% endfor %}


# Archived editions

{% assign files = site.static_files | where: "extname", ".pdf" | sort: "path" %}
{% assign current_year = "" %}

{% for f in files %}
  {% if f.path contains "/editions/" %}
    {% assign parts = f.path | split: "/" %}
    {% assign year  = parts[2] %}

    {% if year != current_year %}
## {{ year }}
{% assign current_year = year %}
{% assign base       = "/editions/" | append: year | append: "/" %}
{% assign main       = base | append: "forallxbris.pdf" %}
{% assign accessible = base | append: "forallxbris-accessible.pdf" %}
{% assign answers    = base | append: "forallxbris-withanswers.pdf" %}

{% for item in files %}{% if item.path == main %}- <a href="{{ item.path | relative_url }}">{{ item.name }}</a>
{% endif %}{% endfor %}
{% for item in files %}{% if item.path == accessible %}- <a href="{{ item.path | relative_url }}">{{ item.name }}</a>
{% endif %}{% endfor %}
{% for item in files %}{% if item.path == answers %}- <a href="{{ item.path | relative_url }}">{{ item.name }}</a>
{% endif %}{% endfor %}
    {% endif %}

    {% if f.path != main and f.path != accessible and f.path != answers %}
- <a href="{{ f.path | relative_url }}">{{ f.name }}</a>
    {% endif %}
  {% endif %}
{% endfor %}
