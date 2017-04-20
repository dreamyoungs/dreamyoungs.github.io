---
layout: post
title:  "My First Blog Post"
date:   2015-01-12 23:25:05
author: Mahabub Islam
categories: Blog
image: true
comments: yes
---


{% if page.image %}
<div class="post-img">
<img class="img-responsive img-post" src=" {{site.baseurl}}/public_html/img/tiger.jpeg "/>
</div>
{% endif %}



<!-- {% if page.fbcomments %}
    <hr/>
    <h4>Comments</h4>
    <div class="fb-comments" data-href="http://joshuacox.github.io{{ page.url }}" data-colorscheme="dark" data-num-posts="4" data-width="706"></div>
{% endif %} -->
