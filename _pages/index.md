---
layout: defaults/page
permalink: index.html
narrow: true
title: KEIWIKI에 오신 것을 환영합니다.
---

## 페이지의 목적

{% include components/intro.md %}

[여기에 해당 문서의 상세한 설명이 제시되어 있습니다.]({{ site.baseurl}}{% link _pages/about.md %})

## 페이지의 사용 방법
해당 문서의 개시글들은 마크다운 문법으로 작성합니다.

[Documentation]({{ site.baseurl }}{% link list/projects.md %})에는 이 문서에서 다루는 주제들과 그 주제들에 대한 간단한 설명들이 배치될 것입니다.

그리고 각각에 대한 고찰이나 상세한 설명 등은 [Posts]({{ site.baseurl }}{% link list/posts.html %})에 배치될 것이며 Documentation에 링크가 배치될 예정입니다.

<hr />

### Recent Posts

{% for post in site.posts limit:3 %}
{% include components/post-card.html %}
{% endfor %}


