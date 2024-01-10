---
layout: default
title: "Blog"
categories:
  - Knowledge
  - IGC
  - Project
  - Future-Project
---

{% for cat in page.categories %}
<h1>{{ cat }}</h1>
  {% for post in site.categories[cat] %}
  <h3>{{ post.title }}</h3>
  <p style="margin-top:-1em; color:#aaa;"><small>{{ post.date | date: "%-d %B %Y" }}</small></p>
  <p>{{ post.description }}. <a href="{{ post.url }}">Mehr</a></p>
  {% endfor %}  
{% endfor %}
