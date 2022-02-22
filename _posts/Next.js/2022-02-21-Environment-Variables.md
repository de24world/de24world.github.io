---
layout: single
title: "Environment Variables(환경변수)"
categories: Next.js
tag: [Environment, env, next.js]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

Next.js에는 환경 변수에 대한 지원이 내장되어 있어 다음을 수행할 수 있습니다.

- [`.env.local` 환경 변수를 로드하는 데 사용](#환경-변수-로드)
- [`NEXT_PUBLIC_` 접두사를 사용하여 브라우저에 환경 변수를 노출합니다.]()

# 환경 변수 로드

Next.js에는 `.env.local`에서 `process.env`로 환경 변수를 로드하는 기능이 내장되어 있습니다.

예 `.env.local`:

```
DB_HOST=localhost
DB_USER=myuser
DB_PASS=mypassword
```

이렇게 하면 `process.env.DB_HOST`, `process.env.DB_USER` 및 `process.env.DB_PASS`가 Node.js 환경에 자동으로 로드되어 [Next.js 데이터 가져오기 메서드](https://nextjs.org/docs/basic-features/data-fetching/overview) 및 [API 경로](https://nextjs.org/docs/api-routes/introduction)에서 사용할 수 있습니다.

예를 들어, `getStaticProps` 사용한다면:

```js
// pages/index.js
export async function getStaticProps() {
  const db = await myDB.connect({
    host: process.env.DB_HOST,
    username: process.env.DB_USER,
    password: process.env.DB_PASS,
  });
  // ...
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

- [Data fetching (서버사이드와 클라이언트 사이드 조합)](<https://serzhul.io/REACT/data-fetching-(%EC%84%9C%EB%B2%84%EC%82%AC%EC%9D%B4%EB%93%9C%EC%99%80-%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8-%EC%82%AC%EC%9D%B4%EB%93%9C-%EC%A1%B0%ED%95%A9)/>)
- [](https://cpro95.tistory.com/492)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
