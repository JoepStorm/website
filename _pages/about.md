---
permalink: /
title: ""
author_profile: false
redirect_from:
  - /about/
  - /about.html
---

{% include base_path %}

<div class="home-hero" style="text-align:center; margin: 0.5em auto 1.2em; max-width: 720px;">
  <img src="{{ site.author.avatar | prepend: '/images/' | prepend: base_path }}"
       alt="{{ site.author.name }}"
       style="width: 200px; height: 200px; border-radius: 50%; object-fit: cover; margin-bottom: 0.3em;" />
  <h1 style="margin: 0.1em 0;">{{ site.author.name }}</h1>
  {% if site.author.bio %}<p style="font-size: 1.05em; color: var(--global-muted-color, #555);">{{ site.author.bio }}</p>{% endif %}
</div>

Hi, I'm Joep. I'm a PhD candidate in Delft working on machine learning for computational mechanics.
I'm focusing on accelerating physics-based simulations with machine-learning based techniques without sacrificing robustness.
During my PhD, I've had research collaborations with Columbia and Aarhus University.

Next to my work on computational mechanics, I've also been drawn to technical AI Safety.
I've organized programs at the Delft AI Safety Initiative, and worked on several projects, such as AI Safety Camp and the Dutch AI Safety project competition.

## Updates

<ul class="updates-list" style="list-style:none; padding:0;">
{% assign sorted_updates = site.data.updates | sort: 'date' | reverse %}
{% for update in sorted_updates %}
  <li style="padding: 0.6em 0; border-bottom: 1px solid var(--global-border-color, #eee);">
    <span style="display:inline-block; min-width: 6.5em; color: var(--global-muted-color, #888); font-variant-numeric: tabular-nums;">{{ update.date | date: "%Y-%m-%d" }}</span>
    {% if update.link %}<a href="{{ update.link | relative_url }}"><strong>{{ update.title }}</strong></a>{% else %}<strong>{{ update.title }}</strong>{% endif %}
    {% if update.body %}
      <div style="margin: 0.2em 0 0 6.5em; color: var(--global-text-color, #444);">{{ update.body | markdownify }}</div>
    {% endif %}
  </li>
{% endfor %}
</ul>
