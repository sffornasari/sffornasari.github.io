---
layout: archive
title: Others
permalink: /Others
author_profile: true
---

{% include group-by-array collection=site.posts field='categories' %}
<div>
  {% for tag in group_names %}
    {% if tag == 'Others' %}
      {% assign posts = group_items[forloop.index0] %}
      <ul>
        {% for post in posts %}
        <li>
          <a href='{{ site.baseurl }}{{ post.url }}'>{{ post.title }}</a>
        </li>
        {% endfor %}
      </ul>
    {% endif %}
  {% endfor %}
</div>

