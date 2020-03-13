---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: custom
title: "Home Page"
---

<!-- Recent News -->
<h1>Recent News</h1>
<ul>
  <li>Our poster on Edge based Cellular Networks has been accepted at SigComm 2019, Beijing.</li>
</ul>

<h1>Recent Blogs</h1>
{% for post in site.posts limit:5 %}
<a href="{{ post.url }}">{{ post.title }}</a> <br>
{% endfor %}