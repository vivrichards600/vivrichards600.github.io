---
layout: page
permalink: /about/index.html
title: Viv Richards
tags: [Viv, Richards]
imagefeature: viv.jpg
chart: true
---
Not the cricketer! I am the Lead QA consultant at <a href="http://rubberduckconsulting.co.uk/" target="_blank">Rubber Duck Consulting</a>, an International speaker, conference organiser and facilitator. In my spare time I enjoy teaching children to code as a CodeClub volunteer as well as spending time with my wife, 5 children, chicken and dog.

<figure>
  <img src="{{ site.url }}/images/viv.jpg" alt="Viv Richards">
  <figcaption>Viv Richards</figcaption>
</figure>

{% include counteventdetails.html %} 

{% assign total_words = 0 %}
{% assign total_readtime = 0 %}
{% assign featuredcount = 0 %}
{% assign statuscount = 0 %}

{% for post in site.posts %}
    {% assign post_words = post.content | strip_html | number_of_words %}
    {% assign readtime = post_words | append: '.0' | divided_by:200 %}
    {% assign total_words = total_words | plus: post_words %}
    {% assign total_readtime = total_readtime | plus: readtime %}
    {% if post.featured %}
    {% assign featuredcount = featuredcount | plus: 1 %}
    {% endif %}
{% endfor %}

<a href="{{ site.url }}/events">Click here to view the full list of events I've spoken at or will be speaking at shortly.</a>