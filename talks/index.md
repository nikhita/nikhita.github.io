---
layout: page
title: Talks
permalink: /talks/
---
<br>
A list of talks that I have presented at various conferences. 
I have just started with tech speaking but when I was on stage, I realized it was extremely **FUN** and that I want to do more of this!

<div>
{% for talks in site.talks reversed %}
  {% if talks.date > site.time %}
    {% if forloop.first %}
      <h2 class="talks-section" id="upcoming">Upcoming</h2>
    {% endif %}
  {% else %}
    {% assign currentyear = talks.date | date: "%Y" %}
    {% if currentyear != previousyear %}
      <h2 class="talks-section" id="y{{ talks.date | date: "%Y"}}">{{ currentyear }}</h2>
      {% assign previousyear = currentyear %}
    {% endif %}
  {% endif %}


    <div class="talks">
      <span class="post-title"><strong><big> {{ talks.title }} - </big></strong></span>
      {% if talks.subtitle %}
      <span class="post-date talks-subtitle"> {{ talks.subtitle }} </span>
      {% endif %}
      <br>

      <i class="fa fa-comments-o" aria-hidden="true"></i>
      {% if talks.event-url %}
      <a href="{{ talks.event-url }}"
       title="{% if talks.event-fulltitle %}{{ talks.event-fulltitle }}{% else %}{{ talks.event }}{% endif %}
{{ talks.event-url }}">
      {% endif %}

      {{ talks.event }}{% if talks.event-fulltitle %}: {{ talks.event-fulltitle }}{% endif %}
      {% if talks.event-url %}</a>{% endif %}
      <br>

      <span class="location">
        <i class="fa fa-map-marker" aria-hidden="true"></i>
        {{ talks.location }}
      </span>
      <br>

      <i class="fa fa-calendar" aria-hidden="true"></i> {{ talks.date | date: "%B %-d, %Y" }}
      <br>

      {% if talks.slides %}
        <span class="talks-resource">
          <i class="fa fa-file-pdf-o" aria-hidden="true"></i>
          {% if talks.slides contains ".pdf" %}
            <a href="{{ site.pdfs }}/{{ talks.slides }}">
          {% else %}
            <a href="{{ talks.slides }}">
          {% endif %}
          Slides</a>
        </span>
      {% endif %}
      
      {% if talks.video %}
        &nbsp; &nbsp;
        <span class="talks-resource"><i class="fa fa-file-video-o" aria-hidden="true"></i> <a href="{{ talks.video }}">Video</a></span>
      {% endif %}
      
      {% if talks.post %}
        &nbsp; &nbsp;
        <span class="talks-resource">
          <i class="fa fa-file-text-o" aria-hidden="true"></i>
          <a href="{{ site.url }}{{ talks.post }}">Post</a>
        </span>
      {% endif %}
  
      {% if talks.news %}
        &nbsp; &nbsp;
        <span class="talks-resource"><i class="fa fa-file-text-o" aria-hidden="true"></i> <a href="{{ talks.news }}">Featured</a></span>
      {% endif %}
    </div>
{% endfor %}
</div>

