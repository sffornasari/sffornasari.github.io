---
layout: page
title: Other
permalink: /other
---

{% include group-by-array.html collection=site.posts field='categories' %}

<ul>
  {% for tag in group_names %}
    {% if tag == 'other' %}
      {% assign posts = group_items[forloop.index0] %}
    {% endif %}
    <li>
      <h2>{{ tag }}</h2>
      <ul>
        {% for post in posts %}
        <li>
          <a href='{{ site.baseurl }}{{ post.url }}'>{{ post.title }}</a>
        </li>
        {% endfor %}
      </ul>
    </li>
  {% endfor %}
</ul>
