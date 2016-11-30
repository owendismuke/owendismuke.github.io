---
layout: page
title: Blog Archive
permalink: /archive/
banner_image: sample-banner-image-3.jpg
---

<div>
{% for post in site.posts %}
  {% capture currentyear %}{{post.date | date: "%Y"}}{% endcapture %}
  {% if currentyear <> year %}
    {% if forloop.first <> true %} 
    </ul>
    {% endif %}
    <h5>{{ currentyear }}</h5>
    <ul>
    {% capture year %}{{currentyear}}{% endcapture %} 
  {% endif %}
      <li><a href="{{ post.url | prepend: site.url }}">{{ post.title }}</a></li>
{% endfor %}
    </ul>
</div>