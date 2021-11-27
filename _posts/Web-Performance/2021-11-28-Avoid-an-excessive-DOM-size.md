---
layout: single
title: "Avoid an excessive DOM size"
categories: Web-Performance
tag: [DOM, lazy-loading, infinite-scrolling, content-visibility]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

대부분 외부 라이브러리에서 불러올 때 해당 문제가 많이 발생한다. (예: slider 라이브러리 등) 왜냐하면 외부 라이브러리에는 많은 스타일링과 div 요소(즉 DOM node)가 이미 작성되어 있기 때문에 DOM 깊이(Depth)와 Child Element(자식 요소)들이 포함되어 있기 때문이다.

<img src="/assets/images/CLS/width_height.gif" />

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>1. </li>
  <li>2. </li>
  <li>3. </li>
</ul>
</div>

#### 참고 영상

- [Github 블로그](https://youtu.be/q0P3TSoVNDM){% include video id="q0P3TSoVNDM" provider="youtube" %}

#### 참조 문서 및 사이트

- [How to Reduce the Number of DOM Elements](https://www.oscprofessionals.com/blog/how-to-reduce-the-number-of-dom-elements/)
- [](https://frontdev.tistory.com/entry/content-visibility-%EB%A0%8C%EB%8D%94%EB%A7%81-%EC%84%B1%EB%8A%A5%EC%9D%84-%ED%96%A5%EC%83%81%EC%8B%9C%ED%82%A4%EB%8A%94-%EC%83%88%EB%A1%9C%EC%9A%B4-CSS-%EC%86%8D%EC%84%B1)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
