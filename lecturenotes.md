---
layout: page
title: Lecture notes
---



<ul>
  {% for lecturenotes in site.lecturenotes %}
   <!--  <li>
      <h2>{{ lecturenotes.title }}</h2>
       <p>{{ lecturenotes.content | markdownify }}</p>
    </li> -->
<li>
      <h2><a href="{{ lecturenotes.url | relative_url }}">{{ lecturenotes.title }}</a></h2>
         </li>

     
  {% endfor %}
</ul>
