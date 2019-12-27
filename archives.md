---
layout: page
permalink: archives/
title: "Archives"
---

<!-- http://alanwsmith.com/jekyll-liquid-date-formatting-examples -->

{% assign current_year = "" %}
{% assign current_month = "" %}

{% for post in site.posts %}

  {% capture year %}{{ post.date | date: "%Y" }}{% endcapture %}
  {% if current_year != year %}
    {% assign current_year = year %}
    {% assign current_month = "" %}
## {{ year }}
  {% endif %}

  {% capture month %}{{ post.date | date: "%m" }}{% endcapture %}
  {% if current_month != month %}
    {% assign current_month = month %}
### {% case month %}
      {% when "01" %}Janvier
      {% when "02" %}Février
      {% when "03" %}Mars
      {% when "04" %}Avril
      {% when "05" %}Mai
      {% when "06" %}Juin
      {% when "07" %}Juillet
      {% when "08" %}Août
      {% when "09" %}Septembre
      {% when "10" %}Octobre
      {% when "11" %}Novembre
      {% when "12" %}Décembre
    {% endcase %} {{ post.date | date: " %Y" }}
  {% endif %}

* [{{ post.title }}]({{ post.url | relative_url }})
{% endfor %}
