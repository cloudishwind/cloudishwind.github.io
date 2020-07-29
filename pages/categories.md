---
layout: page
title: Categories
---

<div class="page">
  <span>
    {% for category in site.categories %}
      {% if category != "project" %}
        &nbsp;&nbsp;<a href="#{{ category[0] | slugify }}">{{ category[0] }}({{ category[1].size }})</a>
      {% endif %}
    {% endfor %}
  </span>
  
  <hr/>
  
  {% for category in site.categories %}
    {% if category != "project" %}
      <h2 id="{{ category[0] | slugify }}">{{ category[0] }}</h2>
      <ul class="related-posts">
        {% for post in category[1] %}
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
     {% endif %}
  {% endfor %}
</div>
