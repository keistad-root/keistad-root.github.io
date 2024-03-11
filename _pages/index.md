---
layout: defaults/page
permalink: index.html
narrow: true
title: KEIWIKI에 오신 것을 환영합니다.
---

## Purpose of website

{% include components/intro.md %}

[For more details, click me.]({{ site.baseurl}}{% link _pages/about.md %})

<hr />

### Recent Posts

{% for post in site.posts limit:3 %}
{% include components/post-card.html %}
{% endfor %}


