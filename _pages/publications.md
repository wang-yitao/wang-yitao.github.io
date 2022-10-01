---
layout: page
permalink: /publications/
title: Publications
subtitle: Please see <a href="https://bit.ly/cy-gs">Google Scholar</a> for the up-to-date list.

years: [2022, 2021]
nav: true
nav_order: 1
---
<!-- _pages/publications.md -->
<div class="publications">

{%- for y in page.years %}
  <h2 class="year">{{y}}</h2>
  {% bibliography -f papers -q @*[year={{y}}]* %}
{% endfor %}

</div>
