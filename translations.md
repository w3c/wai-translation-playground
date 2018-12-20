---
title: "Translations"
permalink: /translations/
layout: default
github:
  repository: w3c/wai-translation-playground
  path: translations.md
---

{% assign languages=site.documents | where_exp:"item", "item.lang != 'en'" | sort: 'lang' | map: "lang" | uniq %}


{%- for l in languages %}
{% if l %}
{% include excol.html type="start" id=l %}
<span lang="{{l}}" bidi="auto">{{ site.data.lang[l].nativeName }}</span> ({{ site.data.lang[l].name }})
{% include excol.html type="middle" %}
  {% assign pages=site.documents | where: "lang", l | sort: "title" %}
  {% for p in pages %}
    {%- if forloop.first %}<ul lang="{{l}}">{% endif -%}
      <li><a href="{{ p.url | relative_url }}">{{ p.title }}</a></li>
    {%- if forloop.last  %}</ul>{% endif -%}
  {% endfor%}
{% include excol.html type="end" %}
{% endif %}
{% endfor -%}