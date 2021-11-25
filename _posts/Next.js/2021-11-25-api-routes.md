---
layout: single
title: "Next.js API Routes"
categories: Next.js
tag: [Next.js, API, Routes]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

<div class="notice">
<h2>예시</h2>
<ul>
  <li><a href="https://github.com/vercel/next.js/tree/canary/examples/api-routes">Basic API Routes </a></li>
  <li><a href="https://github.com/vercel/next.js/tree/canary/examples/api-routes-middleware">API Routes with middleware </a></li>
  <li><a href="https://github.com/vercel/next.js/tree/canary/examples/api-routes-graphql">API Routes with GraphQL </a></li>
  <li><a href="https://github.com/vercel/next.js/tree/canary/examples/api-routes-rest">API Routes with REST </a></li>
  <li><a href="https://github.com/vercel/next.js/tree/canary/examples/api-routes-cors">API Routes with CORS </a></li>

</ul>
</div>

## API Routes란?

- `API(Application Programming Interface)`는 API는 컴퓨터나 컴퓨터 프로그램 사이의 연결이다. 일종의 소프트웨어 인터페이스이며 다른 종류의 소프트웨어에 서비스를 제공한다. 이러한 연결이나 인터페이스를 빌드하거나 사용하는 방법을 기술하는 문서나 표준은 API 사양으로 부른다.쉽게 말해 사용자와 상품 개발자 사이를 이어주는 `사용설명서`라고 보면 된다. 인터페이스는 컴퓨터나 기계간의 정보 교환하기 위한 수단이나 방법을 의미한다. `Routes`는 `경로`라는 의미로써 여기서는 `URL 경로`라고 생각하면 된다.

API routes 는 당신의 Next.js의 API 빌드 솔루션(해결책)을 제공합니다.

`pages/api` 폴더에 있는 모든 파일들은 `/api/\*` 매핑되어, `page`가 아닌 API Endpoint 로 처리됩니다. 해당 bundles(번들들은) 오직 server-side 이며 client-side 번들 사이즈를 증가시키지 않습니다.

에를 들어, `pages/api/user.js` 해당 API route는 `200` 상태 코드인 `json` 반환시킵니다.

```js
export default function handler(req, res) {
  res.status(200).json({ name: "John Doe" });
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

- [API Routes 공식홈페이지](https://nextjs.org/docs/api-routes/introduction)
- [NextJS API Routes](https://serzhul.io/REACT/nextjs-api-routes/)
- [](https://ohhako.github.io/kimhako/articles/2020-11/Nextjs-attractive-post)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
