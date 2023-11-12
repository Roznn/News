---
layout: page
title: Lecture notes
permalink: /lecturenotes/
---

# Module CS007

- [first tutorial](exampletutorial.md)

- [second tutorial](exampletutorial2.md)

# Module ST007


<ul>
  {% for lecturenotes in site.lecturenotes %}
    <li>
      <h2>{{ lecturenotes.author }}</h2>
      <h3>{{ lecturenotes.date }}</h3>
      <p>{{ lecturenotes.content | markdownify }}</p>
    </li>
  {% endfor %}
</ul>