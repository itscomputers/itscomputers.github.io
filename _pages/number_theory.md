---
layout: page
title: number theory for programmers
nav_title: number theory
nav: true
position: 1
permalink: /number_theory
---

<div class="sections">
  <ul class="section-list">
    {% assign
      sections = site.pages
        | where: "category", "number theory"
        | sort: "section"
    %}
    {% for node in sections %}
    <li class="section-list-item">
      {{ node.chapter }}.{{ node.section }} -
      <a href="{{ node.url | prepend: site.baseurl }}">{{ node.title }}</a>
    </li>
    {% endfor %}
  </ul>
</div>

