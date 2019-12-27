---
layout: default
title: Archives
permalink: archives/
---

<!-- http://alanwsmith.com/jekyll-liquid-date-formatting-examples -->

{% assign current_year = "" %}
{% assign current_month = "" %}

{% for post in site.posts %}

  {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
  {% if current_year != year %}
    {% assign current_year = year %}
    {% assign current_month = "" %}
## {{ year }}
  {% endif %}

  {% capture month %}{{ post.date | date: '%m' }}{% endcapture %}
  {% if current_month != month %}
    {% assign current_month = month %}
### {{ post.date | date: '%B %Y' }}
  {% endif %}

* [{{ post.title }}]({{ post.url | relative_url }})
{% endfor %}
