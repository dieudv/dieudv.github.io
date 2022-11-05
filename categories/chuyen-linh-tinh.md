---
layout: page
title: Chuyện linh tinh
permalink: /blog/categories/chuyen-linh-tinh/
---

<h5> Posts by Category : {{ page.title }} </h5>

<div class="card">
{% for post in site.categories.chuyen-linh-tinh %}
 <li class="category-posts"><span>{{ post.date | date_to_string }}</span> &nbsp; <a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
</div>