---
title: Documentation
layout: collection
permalink: /manpages/
collection: manpages
classes: wide
---


<ul>
  {% for manpage in site.manpages %}
    <li>
        <a href="{{ manpage.url }}">{{ manpage.coll_name }}</a> - {{ manpage.coll_desc }}
    </li>
  {% endfor %}
</ul>

