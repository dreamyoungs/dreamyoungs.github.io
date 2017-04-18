---
layout: post
title:  "My First Blog Post"
date:   2015-01-12 23:25:05
author: Mahabub Islam
categories: Blog
image: true
comments: false
---


{% if page.image %}
<div class="post-img">
<img class="img-responsive img-post" src=" {{site.baseurl}}/public_html/img/tiger.jpeg "/>
</div>
{% endif %}




{% if page.comments %}  {% endif %}
