---
layout: default
---

# Home

Welcome to **hulles**, where I keep stuff not related to specific projects, like my GitHub blog. 

## Projects

### A1icia

[A1icia](https://github.com/markhull/A1icia.git) is a personal assistant written in Java. She is modular, extensible, and damn fast.

### simpler-word2vec

[simpler-word2vec](https://github.com/markhull/simpler-word2vec.git) is a simple and reasonably efficient toolbox for using large word2vec datasets written in Java.

## Posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
