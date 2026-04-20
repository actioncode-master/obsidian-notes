---
title: "AI"
layout: page
category: ai
permalink: /ai/
---

# AI

이 페이지는 AI 관련 포스팅들의 인덱스입니다. 아래 목록은 `ai` 카테고리에 속한 포스트만 표시됩니다.

<ul>
{% for post in site.posts %}
  {% if post.categories contains 'ai' %}
    <li><a href="{{ post.url | relative_url }}">{{ post.title }}</a> — {{ post.date | date: "%Y-%m-%d" }}</li>
  {% endif %}
{% endfor %}
</ul>
