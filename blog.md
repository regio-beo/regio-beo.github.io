---
layout: default
title: "Blog"
categories:
  - Knowledge
  - IGC
---

{% for cat in page.categories %}
<h1>{{ cat }}</h1>
  {% for post in site.categories[cat] %}
  <h3>{{ post.title }}</h3>
  <p>{{ post.description }} <a href="{{ post.url }}">Weiterlesen</a>.</p>
  {% endfor %}  
{% endfor %}
