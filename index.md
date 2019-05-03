---
layout: default
title: Home
---

# [Home Page]

<center><h2><Features🌹置、顶\></h2></center>

{% for post in site.posts %}
{% if post.top == true %}

---

<center><h2>{{ post.title }}</h2></center>

{{ post.excerpt }}

Click for [>more\<]({{ post.url }})

---

{% endif %}
{% endfor %}

<center>οΟ○     の     ○Οο…·～·……·～·…οΟ○     の     ○Οο</center>

<center><h2><Latest🌸Posts\></h2></center>

{% for post in site.posts %}

---

<center><h2>{{ post.title }}</h2></center>

{{ post.excerpt }}

Click for [>more\<]({{ post.url }})

---

{% endfor %}
