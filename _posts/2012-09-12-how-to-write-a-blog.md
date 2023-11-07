---
layout: post
title:  "how to use data from CSV"
date:   2012-09-12 19:41:59 +0000
categories: jekyll update
---

# Welcome

The data below is read directly from [test.csv](_data/test.csv)
to generate a list of peoplename  with urls:

<ul>
{% for test in site.data.test %}
  <li>
    <a href="{{ test.url }}">
      {{ test.name }}
    </a>
  </li>
{% endfor %}
</ul>