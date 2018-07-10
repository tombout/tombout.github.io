---
layout: default
title: home
---

{% for post in site.posts %}
<section>
    <h3><a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></h3>
    <p><small>{{ post.date | date_to_string }}</small> {{ post.description }}</p>
</section>
{% endfor %}
