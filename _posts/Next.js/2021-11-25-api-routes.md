---
layout: single
title: "Next.js API Routes"
categories: Next.js
tag: [Next.js, API, Routes, Dynamic API Routes, Rest API]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# API Routes란?

- [REST API가 뭔가요?](https://youtu.be/iOueE9AXDQQ){% include video id="iOueE9AXDQQ" provider="youtube" %}

- `API(Application Programming Interface)`는 API는 컴퓨터나 컴퓨터 프로그램 사이의 연결이다. 일종의 소프트웨어 인터페이스이며 다른 종류의 소프트웨어에 서비스를 제공한다. 이러한 연결이나 인터페이스를 빌드하거나 사용하는 방법을 기술하는 문서나 표준은 API 사양으로 부른다.쉽게 말해 사용자와 상품 개발자 사이를 이어주는 `사용설명서`라고 보면 된다. 인터페이스는 컴퓨터나 기계간의 정보 교환하기 위한 수단이나 방법을 의미한다. `Routes`는 `경로`라는 의미로써 여기서는 `URL 경로`라고 생각하면 된다.

## 예시

<div class="notice">
<ul>
  <li><a href="https://github.com/vercel/next.js/tree/canary/examples/api-routes">Basic API Routes </a></li>
  <li><a href="https://github.com/vercel/next.js/tree/canary/examples/api-routes-middleware">API Routes with middleware </a></li>
  <li><a href="https://github.com/vercel/next.js/tree/canary/examples/api-routes-graphql">API Routes with GraphQL </a></li>
  <li><a href="https://github.com/vercel/next.js/tree/canary/examples/api-routes-rest">API Routes with REST </a></li>
  <li><a href="https://github.com/vercel/next.js/tree/canary/examples/api-routes-cors">API Routes with CORS </a></li>

</ul>
</div>

API routes 는 당신의 Next.js의 API 빌드 솔루션(해결책)을 제공합니다.

`pages/api` 폴더에 있는 모든 파일들은 `/api/\*` 매핑되어, `page`가 아닌 API Endpoint 로 처리됩니다. 해당 bundles(번들들은) 오직 server-side 에서만 번들되어, client-side 번들 사이즈를 증가시키지 않습니다.

에를 들어, `pages/api/user.js` 해당 API route는 `200` 상태 코드인 `json` 반환시킵니다.

```js
export default function handler(req, res) {
  res.status(200).json({ name: "John Doe" });
}
```

API 라우터가 작동하기 위해서는 default 함수(request handler 라 불리는)를 export 해야하며, 아래와 같은 파라미터를 가집니다.

- `req`: [http.incomingMessage](https://nodejs.org/api/http.html#http_class_http_incomingmessage) 인스턴스이다. 미들웨어로 적용하고 싶다면 [Api-middlewares](https://nextjs.org/docs/api-routes/api-middlewares)를 살펴보세요.
- `res`: [http.ServerResponse](https://nodejs.org/api/http.html#http_class_http_serverresponse) 인스턴스이다. [Response helper 함수](https://nextjs.org/docs/api-routes/response-helpers) 를 살펴보면 더 좋습니다.

서로 다른 HTTP 메서드를 API 라우터에서 다루기 위해 `req.method` 를 request handler 안에서 사용할 수 있습니다.

```js
export default function handler(req, res) {
  if (req.method === "POST") {
    // POST request 처리
  } else {
    // 그 외의 다른 HTTP method
  }
}
```

API 엔드포인트 fetch하기 위해서는 이 페이지의 [상단 시작 부분](#예시)에 있는 예제를 참조하세요.

## 사용 사례

새로운 프로젝트인 경우, API 라우터를 사용해 전체 API 를 빌드할 수 있습니다. 만약 API 가 이미 존재한다면, API 라우터로 API 를 호출할 필요는 없습니다. API 라우터의 다른 사례는 다음과 같습니다.

- 외부 서비스의 URL 마스킹 할 수 있습니다.(https://domain.com/secret-url -> /api/secret)
- 서버의 [환경변수](https://nextjs.org/docs/basic-features/environment-variables)를 사용해 외부 서비스에 안정적으로 접근할 수 있습니다.

## 주의사항

- API 라우터는 [CORS 헤더를 지정하지 않습니다](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS). 이는 기본적으로 오직 `same-origin` 만 있음을 뜻합니다. 동작(behavior) 커스터마이징하고 싶다면 [CORS 미들웨어](https://nextjs.org/docs/api-routes/api-middlewares#connectexpress-middleware-support) 를 request handler 에 래핑하면 됩니다.
- API 라우터는 `next export` 에서 사용할 수 없습니다.

# Dynamic API Routes

## 예시

<div class="notice">
<ul>
  <li><a href="https://github.com/vercel/next.js/tree/canary/examples/api-routes">Basic API Routes </a></li>
</ul>
</div>

API routes는 [dynamic routes](https://nextjs.org/docs/routing/dynamic-routes) 지원하고,동일한 파일 명명 규칙을 `pages`에 따릅니다.

예를 들어 API route(경로) `pages/api/post/[pid].js` 에는 다음 코드가 있습니다.

```js
export default function handler(req, res) {
  const { pid } = req.query;
  res.end(`Post: ${pid}`);
}
```

이제, `/api/post/abc`에 대한 요청에 `Post: abc`라는 텍스트가 응답할 것입니다.

## Index routes 와 Dynamic API routes

매우 일반적인 RESTful 패턴은 다음과 같이 경로를 설정합니다:

- `GET api/posts` - 페이지가 매겨진 게시물 목록을 얻습니다.
- `GET api/posts/12345` - 게시물 ID 12345를 얻습니다.

이를 두 가지 방법으로 모델링할 수 있습니다.

- 옵션 1:

  - `/api/posts.js`
  - `/api/posts/[postId].js`

- 옵션 2:
  - `/api/posts/index.js`
  - `/api/posts/[postId].js`
    둘 다 같습니다. 세번째 옵션으로 오직 `/api/posts/[postId].js`만 쓰는 것은 유효하지 않은데, 왜냐하면 Dynamic Routes(모든 routes 포함 - 아래 참조)에는 `undefined` 상태와 `GET api/posts`는 어떠한 상황에서도 `/api/posts/[postId].js` 매칭 시켜주지 않기 때문입니다.

#### 참고 영상

- [REST API가 뭔가요?](https://youtu.be/iOueE9AXDQQ){% include video id="iOueE9AXDQQ" provider="youtube" %}
- [Next js 강좌 #7 API Routes, 로그인 구현](https://youtu.be/R-IAWcTpNO4){% include video id="R-IAWcTpNO4" provider="youtube" %}
- [Next.js Tutorial - 41 - API Routes](https://youtu.be/aZkZUduCauo){% include video id="aZkZUduCauo" provider="youtube" %}
- [Nextjs Tutorial #3 - API Routes](https://youtu.be/_tXDsZmcjeI){% include video id="R_tXDsZmcjeI" provider="youtube" %}

#### 참조 문서 및 사이트

- [API Routes 공식홈페이지](https://nextjs.org/docs/api-routes/introduction)
- [NextJS API Routes](https://serzhul.io/REACT/nextjs-api-routes/)
- [Next.js 공식 Docs 흝기](https://velog.io/@baramofme/Next.js-%EA%B3%B5%EC%8B%9D-Docs-%ED%9D%9D%EA%B8%B0#api-routes)

[상단으로](#예시){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
