---
layout: single
title: "react window"
categories: coding
tag: [window, react, scrroll, Performance, TBT, DOM]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# React Window

## 사용하는 이유

performance 에서

```javascript
    componentDidMount() {
        window.scrollTo(0, 0);
    }
```

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

- [Avoid an excessive DOM size](https://web.dev/dom-size/)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
