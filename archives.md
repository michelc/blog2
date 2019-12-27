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
      {% when "01" %}Janvier {{ year }}
      {% when "02" %}Février {{ year }}
      {% when "03" %}Mars {{ year }}
      {% when "04" %}Avril {{ year }}
      {% when "05" %}Mai {{ year }}
      {% when "06" %}Juin {{ year }}
      {% when "07" %}Juillet {{ year }}
      {% when "08" %}Août {{ year }}
      {% when "09" %}Septembre {{ year }}
      {% when "10" %}Octobre {{ year }}
      {% when "11" %}Novembre {{ year }}
      {% when "12" %}Décembre {{ year }}
    {% endcase %}
  {% endif %}

* [{{ post.title }}]({{ post.url | relative_url }})
{% endfor %}
