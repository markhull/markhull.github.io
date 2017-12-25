---
layout: default
---

# Home

Welcome to **[hulles](https://markhull.github.io)**. I know you were probably uncertain where you were, since the logo above is so easy to miss. This is where I keep stuff not related to specific projects, like my GitHub blog. See **Posts**, below.

## Hulles Java Style Guide

[The official Java style guide](hulles_style.md) for Hulles projects.

## Projects

### A1icia

[A1icia](https://github.com/markhull/A1icia.git) is a personal assistant written in Java. She is modular, extensible, and damn fast.

### simpler-word2vec

[simpler-word2vec](https://github.com/markhull/simpler-word2vec.git) is a simple and reasonably efficient toolbox for using large word2vec datasets written in Java.

## About Me

[Here's some stuff about me](about.md), like my tie size and favorite boy band.

## Posts

<!--
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
-->

<div class="posts">
  {% for post in site.posts %}
    <article class="post">

      <h3><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h3>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ site.baseurl }}{{ post.url }}" class="read-more">Read More</a>
      
    </article>
  {% endfor %}
</div>
