---
layout: default
title: SinceTIme
---

# [Home Page]

<center><h2><Features🌹置、顶\></h2></center>

{% for post in site.posts %}
{% if post.top == true %}

<div class="article-entry">

<center><h2>{{ post.title }}</h2></center>

<p>{{ post.excerpt }}</p>

<p>Click for <a href="{{ post.url }}">>more<</a></p>

</div>

{% endif %}
{% endfor %}

<center>οΟ○     の     ○Οο…·～·……·～·…οΟ○     の     ○Οο</center>

<center><h2><Latest🌸Posts\></h2></center>

{% for post in site.posts %}

<div class="article-entry">

<center><h2>{{ post.title }}</h2></center>


<p>{{ post.excerpt }}</p>

<p>Click for <a href="{{ post.url }}">>more<</a></p>

</div>

{% endfor %}
