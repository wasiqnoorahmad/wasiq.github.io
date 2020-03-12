---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: "default"
title: "Wasiq Noor's Home Page"
---

<!-- Horizontal table for menu -->
<table style="width: 20%;">
  <tr>
    <th>Publications</th>
    <th>Blogs</th>
    <th>Books</th>
    <th><a href="assets/Wasiq_CV.pdf">CV</a></th>
  </tr>
</table>


<!-- Recent News -->
<h1>Recent News</h1>
<ul>
  <li>Our poster on Edge based Cellular Networks has been accepted at SigComm 2019, Beijing.</li>
</ul>

<h1>Recent Blogs</h1>
{% for post in site.posts limit:5 %}
<a href="{{ post.url }}">{{ post.title }}</a> <br>
{% endfor %}