---
layout: default
title: Portfolio
permalink: /portfolio/
---


{% for post in site.posts %}
  <article class="col-6 col-12-xsmall">
    <a href="{{ post.url }}" class="image fit thumb"><img src="{{ post.image | relative_url }}" alt="" /></a>
    <h3> {{ post.title }} </h3>
    <p> {{ post.subtitle }} </p>
  </article>
{% endfor %}
