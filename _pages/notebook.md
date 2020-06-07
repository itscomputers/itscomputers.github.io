---
layout: page
title: notebook
permalink: /notebook
---

<div class="sections">
  <ul class="section-list">
    {% assign
      entries = site.pages
        | where: "category", "notebook"
        | sort: "title"
    %}
    {% for node in entries %}
    <li class="section-list-item">
      <a href="{{ node.url | prepend: site.baseurl }}">{{ node.title }}</a>
    </li>
    {% endfor %}
  </ul>
</div>
