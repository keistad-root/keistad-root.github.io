---
layout: defaults/page
permalink: index.html
narrow: true
title: Welcome to Keistad's blog
---

## Who is Keistad?

Please don't confuse. Keistad is nickname of me, Choi. Keistad is pronounced with German. I want to study Physics in German. So, I studied German and I want to make German nickname. Keistad isn't real German name, but please pronounce it with German.

## Who am I?
If you want know about me, click [here](/about.html)

<hr />

### Recent Posts

{% for post in site.posts limit:3 %}
{% include components/post-card.html %}
{% endfor %}


