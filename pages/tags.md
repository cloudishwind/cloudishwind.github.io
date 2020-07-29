---
layout: page
title: Tags
---

<div class="page">
  <span>
    {% for tag in site.tags %}
      &nbsp;&nbsp;<a href="#{{ tag[0] | slugify }}">{{ tag[0] }}({{ tag[1].size }})</a>
    {% endfor %}
  </span>
  
  <hr/>
  
  {% for tag in site.tags %}
    <h2 id="{{ tag[0] | slugify }}">{{ tag[0] }}</h2>
    <ul class="related-posts">
      {% for post in tag[1] %}
        <li>
          <h3>
            <a href="{{ site.baseurl }}{{ post.url }}">
              {{ post.title }}
              <small>{{ post.date | date_to_string }}</small>
            </a>
          </h3>
        </li>
      {% endfor %}
    </ul>
  {% endfor %}
</div>
