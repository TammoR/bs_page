---
layout: tammo_main
title: Blog
---

<div class="posts">
  {% for post in site.posts %}
    <article class="post">
      <h1><small><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></small></h1>
      <div class="entry">
        {{ post.excerpt }}
      </div>
	{% if post.excerpt != post.content %}
    <a href="{{ site.baseurl }}{{ post.url }}">Read more</a>
	{% endif %}
    </article>
  {% endfor %}
</div>
