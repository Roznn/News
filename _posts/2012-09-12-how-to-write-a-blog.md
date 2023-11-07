---
layout: post
title:  "how to write a blog"
date:   2012-09-12 19:41:59 +0000
categories: jekyll update
---

# Welcome

**Hello world**, this is my first Jekyll blog post.

I hope you like it!

<ul>
{% for test in site.data.test %}
  <li>
    <a href="{{ test.url }}">
      {{ test.name }}
    </a>
  </li>
{% endfor %}
</ul>