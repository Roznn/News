---
layout: page
title: Lecture notes
permalink: /lecturenotes/
---



<ul>
  {% for lecturenotes in site.lecturenotes %}
    <li>
      <h2>{{ lecturenotes.title }}</h2>
      <p>{{ lecturenotes.content | markdownify }}</p>
    </li>
  {% endfor %}
</ul>