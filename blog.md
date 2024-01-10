---
layout: default
title: "Blog"
categories:
  - Knowledge
  - IGC
  - Project
  - Future-Project
---

<h2>Inhalt</h2>
<ul>
{% for cat in page.categories %}
  <li><a href="#{{ cat }}">{{ cat }}</a></li>
{% endfor %}
</ul>

{% for cat in page.categories %}
<h2 id="{{ cat }}">{{ cat }}</h2>
  {% for post in site.categories[cat] %}
  <h3>{{ post.title }}</h3>
  <p style="margin-top:-1em; color:#aaa;"><small>{{ post.date | date: "%-d %B %Y" }}</small></p>
  <p>{{ post.description }}. <a href="{{ post.url }}">Mehr</a></p>
  {% endfor %}  
{% endfor %}
