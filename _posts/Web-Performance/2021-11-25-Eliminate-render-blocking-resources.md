---
layout: single
title: "Eliminate render blocking resources"
categories: Web-Performance
tag:
  [
    웹퍼포먼스,
    웹성능,
    웹성능개선,
    web performance,
    LCP,
    lighthouse,
    style,
    script,
    coverage,
    Chrome,
    DevTools,
    Minify,
  ]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# 렌더링 차단 리소스 제거(Eliminate render blocking resources)

당신의 Lighthouse 보고서는 모든 URL에서 당신의 페이지의 첫번째 페인트(paint)를 막고 있는 부분을 알게 해줍니다. 목표는 중요한 리소스(resources)들을 인라인하고 중요하지 않은 리소스는 미루고, 사용하지 않는 모든 것을 제거하여 URL 렌더링을 차단하고 있는 영향을 줄이는 것입니다.

<img src="/assets/images/Next.js/Eliminate_render_blocking_resources.png" />

## 어떤 URL이 render-blocking-resources로 표시되는가?

Lighthouse는 다음 두 가지 유형의 render-blocking URL로 표시됩니다: script와 stylesheet 태그들

`<script>` tag :

- 문서의 `<head>` 안에 있는
- `defer`(지연) 속성이 없는
- `async`(비동기) 속성이 없는

`<link rel="stylesheet">` tag :

- `disabled` 속성이 없는. 만약 이 속성이 있으면 브러우저는 스타일시트(stylesheet)를 다운로드 하지 않습니다.
- 사용자의 기기와 구체적으로 일치 하는 `media` 속성이 없는. `media="all`은 렌더링 차단(render-blocking)으로 간주됩니다.

## 중요한 리소스를 식별하는 방법

렌더링 차단 리소스의 영향을 줄이는 첫 번째 단계는, 무엇이 중요하고 무엇이 중요하지 않은지 식별하는 것입니다. [Chrome DevTools 탭](https://developer.chrome.com/docs/devtools/coverage/)을 사용하여 중요하지 않은 CSS 및 JS를 식별합니다. 페이지를 로드하거나 실행할 때, 해당 탭은 사용된 코드외 로드된 코드의 양을 알려줍니다.

<img src="/assets/images/Next.js/chrome_devtools_coverage_tab.png" />

오직 필요한 코드와 스타일만 제공하여 페이지의 용량을 줄일 수 있습니다. 파일을 검사하려면 Source 패널에서 해당 URL을 클릭해주세요. CSS 파일 스타일과 Jaavascript 파일 코드는 두 가지 색상으로 표시됩니다.

녹색 (필수): 첫 번째 페인트에 필요한 스타일. 즉 페이지의 핵심 기능에 중요한 코드입니다.
빨강 (불필요): 즉시 표시되지 않는 콘텐츠에 적용되는 스타일. 페이지의 핵심 기능에서 사용하지 않는 코드입니다.

## 렌더링 차단 스크립트를 제거(Render-blocking scripts)하는 방법

중요한 코드를 식별했으면, 해당 코드를 렌더링 차단 URL `script`에서 HTML 페이지의 인라인 태그로 이동하빈다. 페이지가 로드되면, 페이지의 핵심 기능을 처리하는데 필요한 것을 가지게 될 것입니다.

만약 중요하지 않은 렌더링 차단 URL가 코드에 있으면, URL에 코드를 유지하고 `async` 또는 `defer` 속성으로 URL을 표시할 수 있습니다. ([Javascript를 사용하여 상호 작용 추가](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript) 참조)

전혀 사용되지 않은 코드는 제거해야합니다.([사용하지 않은 코드 제거](https://web.dev/remove-unused-code/) 참조)

## 렌더링 차단 스타일시트(Render-blocking stylesheets) 제거하는 방법

`<script>` 태그를 inline으로 넣는 것과 유사하게, first paint에 필수적인 스타일 요소들의 HTML의 `head` 태그 내부에 `style` 태그를 생성하고 거기에 넣으세요. 그리고 나머지 스타일 요소를 `link` 태그에 `preload`를 사용하여 비동저기적으로 불러오세요.([미사용 CSS 지연](https://web.dev/defer-non-critical-css/) 참조)

[Critical 도구](https://github.com/addyosmani/critical/blob/master/README.md)를 사용하여 "Above the Fold" CSS를 추출하고 인라인하는 프로세스를 자동화하는 것이 좋습니다.

렌더랑 차단 스타일을 제거하는 또 다른 방법은 이러한 스타일을 미디어 쿼리별로 구성된 여러 파일로 분할하는 것입니다. 그런 다음 각 스타일시트 링크에 미디어 속성을 추가합니다. 페이지를 로드할 때 브라우저는 사용자의 장치와 일치하는 스타일시트를 검색하기 위해 first paint만 차단합니다.([렌더링 차단 CSS](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css))

마지막으로 css를 축소, 최소화(minify)하여 공백이나 문자를 제거할 수 있습니다([CSS Minify](https://web.dev/minify-css/)) 이렇게 하면 사용자에게 가능한 가장 작은 번들을 보낼 수 있습니다.

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>Lighthouse 와 Coverage 탭을 이용하여 중요하지 않고 사용하지 않은 코드나 파일을 알 수 있다.</li>
  <li> script 태그는 HTML 페이지 내부 inline으로 넣으세요. 그리고 async 혹은 defer 속성을 사용하세요  </li>
  <li>css 파일을 꼭 minify하영 용량을 줄이고, script 태그처럼 유사하게 style(sheets) 태그들도 HTML head 부분에 style 태그를 생성하고 거기 넣으세요. 그리고 preload난 media 속성을 사용하세요.</li>
</ul>
</div>

#### 참조 문서 및 사이트

- [구글 web dev 가이드](https://web.dev/render-blocking-resources/)
- [웹 성능 개선 (1) - Eliminate Render Blocking Resources](https://polarb-raf.dev/%EC%9B%B9-%EC%84%B1%EB%8A%A5-%EA%B0%9C%EC%84%A0-1-eliminate-render-blocking-resources)
- [Mozilla script 태그](https://developer.mozilla.org/ko/docs/Web/HTML/Element/script)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
