---
title: "All WAI Translations"
permalink: /translations/
layout: default
github:
  repository: w3c/wai-translation-playground
  path: translations.md
---

This page lists translations of Web Accessibility Initiative (WAI) website resources. For translations of Web Content Accessibility Guidelines (WCAG), see [WCAG 2 Translations](https://www.w3.org/WAI/standards-guidelines/wcag/translations/). {% comment %}after we integrate those, then we can delete this paragraph.{% endcomment %}

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
