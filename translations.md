---
title: "Translations"
permalink: /translations/
layout: default
github:
  repository: w3c/wai-translation-playground
  path: translations.md
---

{% assign languages=site.documents | where_exp:"item", "item.lang != 'en'" | sort: 'lang' | map: "lang" | uniq %}
<label for="langselect">Show only translations available in:</label>
<select id="langselect">
  {%- for l in languages %}{% if forloop.first %}<option value="">All</option>{% else %}<option value="{{ l }}">{{ site.data.lang[l].nativeName }}</option>{% endif %}{% endfor -%}
</select>
<button id="langselectbutton">Filter</button>

<table id="langtable" class="dense">
  {% assign pages=site.documents | where: "lang", "en" %}
  <thead>
    <tr>
      <th>Page</th><th>Languages</th>
    </tr>
  </thead>
  <tbody>
    {%- for p in pages %}
    {% assign ps=site.documents | where:"ref", p.ref | where_exp:"item", "item.lang != 'en'" | sort: 'lang' %}
    {% assign langs=ps | map: "lang" %}
    <tr data-languages="{%- for l in langs %}{{ l }} {% endfor -%}">
      <th><a href="{{ p.url | relative_url }}">{{ p.title }}</a></th>
      <td>
        {% for pg in ps %}<a style="" href="{{ pg.url | relative_url }}" lang="{{ pg.lang }}">{{ site.data.lang[pg.lang].nativeName }}</a> {% endfor %}
      </td>
    </tr>
    {% endfor -%}
  </tbody>
</table>

<script>
  function filterTable() {
    var lang = document.querySelector('#langselect').value;
    var tablerows = document.querySelectorAll('#langtable tbody tr');
    if (lang != "") {
      for (var i = 0; i < tablerows.length; i++) {
        tablerows[i].setAttribute('hidden', 'true');
      }
      var tablerows = document.querySelectorAll('#langtable tbody tr[data-languages*="'+ lang + '"]');
      for (var i = 0; i < tablerows.length; i++) {
        tablerows[i].removeAttribute('hidden');
      }
    } else {
      for (var i = 0; i < tablerows.length; i++) {
        tablerows[i].removeAttribute('hidden');
      }
    }
  }
  document.querySelector('#langselect').addEventListener('change', function(event) {
    filterTable();
  });
  document.querySelector('#langselectbutton').addEventListener('click', function(event) {
    filterTable();
  });
</script>