---
# layout: single
comments: true
title: "custom Hooks과 (use)Context(Provider)"
categories: React
tag:
  [React, Context, Custom Hooks, Hooks, 커스텀훅, Provider, 리액트, useContext]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# custom Hook

단일

<img src="/assets/images/Git/mono-repo.jpeg" />

## 언제

- 중복되는 state(useState)나 useEffect 등을 재사용하고 싶을 때, custom Hooks
  예를 들어 fetch가 중복되면 useFetch라는 커스텀훅을 만들 수 있다.

[React JS #13 Custom Hooks - 초보자를 위한 리액트 강좌](https://youtu.be/B70lI2PvRnA){% include video id="B70lI2PvRnA" provider="youtube" %}

## 규칙

- 파일 이름 및 함수명은(네이밍) `use...`로 하자. 예 : useFetch.js

# Context Api(Provider)

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>여러 Repo을 통합하여 관리하고 싶다면 모노레포를 적극 고려해본다</li>
  <li>모노레포를 사용하여 여러 Repo에서 중복하여 사용하고 있는 Eslint나 코드, 패키지를 Root에서 통합 관리하여 수월하다.</li>
</ul>
</div>

#### 참고 영상

- [Yarn Workspaces Setup - Multiple JavaScript Packages (Mono-Repo)](https://youtu.be/gOZSZSabCRY){% include video id="gOZSZSabCRY" provider="youtube" %}

#### 참조 문서 및 사이트

- [React Hooks와 Context를 이용한 설계 패턴](https://www.huskyhoochu.com/react-pattern-hooks-and-contexts/)
- [React Context 와 Hooks 설계](https://chchoing88.github.io/ho_blog/context-hooks.md/)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
