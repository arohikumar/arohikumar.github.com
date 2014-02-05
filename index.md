---
layout: page
title: About Technology, Food and Random Thoughts
tagline: To infinity and beyond!
---
{% include JB/setup %}

## Introduction
Hello everyone! The purpose of this blog is for me to keep track of all the things that I am learning. I hate to admit it, but I have had to go back and reread/redo a lot of work in the near past. If anyone benefits from the things that I have documented, all the better :)  
    
## Post Archive

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

