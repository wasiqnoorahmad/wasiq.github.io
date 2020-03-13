---
layout: custom
title: Blogs
permalink: /blogs/
---

# Blogs

{% for blog in site.posts %}

## {{ forloop.index }}. [{{ blog.title }}]({{ blog.url }})
> {{ blog.summary }}

{% endfor %}

