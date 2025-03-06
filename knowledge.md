---
layout: default
title: "Blog"
categories:
  - Knowledge
---

<h2>Knowledge Base</h2>
Hier sammeln wir diverse Informationen von und für die Regios.

{% for cat in page.categories %}
  {% for post in site.categories[cat] %}
  <h3>{{ post.title }}</h3>
  <p style="margin-top:-1em; color:#aaa;"><small>{{ post.date | date: "%-d %B %Y" }}</small></p>
  <p style="margin-top:-1em;">{{ post.description }}. <a href="{{ post.url }}">Mehr</a></p>
  {% endfor %}  
{% endfor %}
