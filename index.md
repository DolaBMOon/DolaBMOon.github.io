---
layout: default
title: SinceTIme
---

# [Home Page💐主、页]

<center><h2><Features🌹置、顶\></h2></center>

{% for post in site.posts %}
{% if post.top == true %}

<div class="article-entry">

<center><h2>{{ post.title }}</h2></center>

<p>{{ post.excerpt }}</p>

<a href="{{ post.url }}"><div class="circle"></div></a>

</div>

{% endif %}
{% endfor %}

<center>οΟ○     の     ○Οο…·～·……·～·…οΟ○     の     ○Οο</center>

<center><h2><Latest🌸Posts\></h2></center>

{% for post in site.posts %}

<div class="article-entry">

<center><h2>{{ post.title }}</h2></center>


<p>{{ post.excerpt }}</p>

<a href="{{ post.url }}"><div class="circle"></div></a>

</div>

{% endfor %}
