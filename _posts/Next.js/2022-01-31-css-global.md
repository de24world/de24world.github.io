---
layout: single
title: "Global CSS Must Be in Your Custom App"
categories: Next.js
tag: [Next.js, Error, css, sass, 에러]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

<img src="/assets/images/Next.js/global_css_error.png" />

# Global CSS Must Be in Your Custom \<App>

## 왜 이러한 에러가 발생하는가

[`pages/_app.js`](https://nextjs.org/docs/advanced-features/custom-app) 이외의 파일에서 전역 CSS를 가져오려고 했습니다.

글로벌 CSS는 부작용 및 순서 문제로 인해 [Custom <App>](https://nextjs.org/docs/advanced-features/custom-app) 이외의 파일에서 사용할 수 없습니다.

## 해결 방법

이러한 충돌을 피하기 위해서는, 모든 first-party 글로벌 css를 [pages/\_app.js file](https://nextjs.org/docs/advanced-features/custom-app)에서 import하도록 고치세요.

혹은, [CSS 모듈을 통해 로컬 CSS(구성 요소 수준 CSS)를 사용하도록 구성 요소를 업데이트](https://nextjs.org/docs/basic-features/built-in-css-support#adding-component-level-css\)합니다. 이것이 선호하는 접근 방식입니다.

## 예시

[`styles.css`](https://nextjs.org/docs/basic-features/built-in-css-support#adding-a-global-stylesheet)라는 스타일 시트를 고려하십시오.

```css
//styles.css
body {
  font-family: "SF Pro Text", "SF Pro Icons", "Helvetica Neue", "Helvetica",
    "Arial", sans-serif;
  padding: 20px 20px 60px;
  max-width: 680px;
  margin: 0 auto;
}
```

아직 없는 경우 `pages/_app.js` 파일을 만듭니다. 그런 다음 `styles.css` 파일을 가져옵니다.

```js
// pages/_app.js
import "../styles.css";

export default function MyApp({ Component, pageProps }) {
  return <Component {...pageProps} />;
}
```

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>해당 에러메세지가 되었다면, 위의 페이지를 참조한다. </li>
  <li>위의 방식데로 하였는데, 에러가 발생한다면 next 버전을 확인해본다. 11.X.X 버전에서 해당 이슈가 발생해서 리액트 및 next를 최신버전으로 업데이트해보니 해당 에러가 해결되었다 </li>
</ul>
</div>

#### 참조 문서 및 사이트

- [Global CSS Must Be in Your Custom \<App>]https://nextjs.org/docs/messages/css-global()

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
