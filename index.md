---
layout: page
title: 主页
tagline: Supporting tagline
---
{% include JB/setup %}

#### 欢迎来到 Jacob 的Blog.
### 时间线

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


