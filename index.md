---
title: Home
layout: default
---

<p class="lead-in">{{ site.description }}</p>
<div class="home grid">
  {% assign posts = site.posts | sort: 'date' | reverse %}
  {% for post in posts %}
  <div class="post grid-item {% for tag in post.tags %}{{ tag | slugify }} {% endfor %}">
    <a href="{{ post.url }}" class="no-style without-style"><h1 class="post-title">{{ post.title }}</h1></a>
    <div class="post-details">
      <!-- <p class="post-details--date">{{ post.date | date: "%b %-d, %Y" }}</p>
      <p class="post-details--byline">{% if post.author %}By <a href="#" class="without-style">{{ post.author }}</a>{% endif %}</p> -->
      {% for author in site.authors %}
        {% if author.title == post.Author %}
          {% assign author_link = author.url %}
        {% endif %}
      {% endfor %}
      {% assign author_slug = post.Author | slugify %}
      <p class="post-details--byline without-style">By {% if author_link contains author_slug %}<a href="/authors/{{ post.Author | downcase | split: ' ' | join: '-'  }}/" class="without-style">{% endif %}{% if post.Author %}{{ post.Author | markdownify | remove: '<p>' | remove: '</p>'}}{% endif %}{% if author_link contains author_slug %}</a>{% endif %}</p>
      <p class="post-details--tags">Tags: {% for tag in post.tags %}<span class="post-topic"><a href="/tags/?tag={{ tag | downcase | split:' ' | join: '-'}}" class="without-style">{{ tag }}</a></span>{% unless forloop.last %} • {% endunless %}{% endfor %}</p>
    </div>
    {{ post.excerpt }}
    <p class="more"><a class="without-style more-button" href="{{ post.url }}"><svg class="svg-more" viewBox="0 0 157 157" preserveAspectRatio="xMinYMax meet"><use xlink:href="#more"></use></svg>READ MORE</a></p>
    {% unless forloop.last %}<hr>{% endunless %}
  </div>
  {% endfor %}

</div>
