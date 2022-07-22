---
layout: single
title: "구글 태그 매니저(GTM)"
categories: Tools
tag:
  [
    GTM,
    Google Tag Manager,
    GTA,
    GA,
    Google Analytic,
    구글 태그 매니저,
    Google Tag Assistant,
  ]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# GTM(Google Tag Manager, 구글 태그 매니저)

## GTM vs gtag.js

| 구분 | Google Tag Manager                         | gtag.js                                   |
| ---- | ------------------------------------------ | ----------------------------------------- |
| 정의 | 웹/웹 추적코드 관리시스템                  | 웹페이지에 직접 추가하는 자바스크립트 F/W |
| 특징 | 웹 인터페이스에서 웹앱 태그 수정 및 배포용 | 직접 설치/운영, 자바스크립트 작업이 중요  |
| 사용 | 중대형 웹사이트                            | 중소형                                    |
| 공통 | 구글 범용 제품에 적용 관리 가능            |

## data Layer

<img src="/assets/images/Tools/tag-manager-server-share.png" />

## 사용법 및 확인법

### console.log로 확인하기

console.log에서 `dataLayer`를 입력하면 값을 손쉽게 확인할 수 있다.
<img src="/assets/images/Tools/data-layer-developer-tools-console.png" />

### Chrome Extension - Google Tag Assistant 으로 확인하기

- 다운로드
  [유용한 도구 Google Tag Assistant 알아보기](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=opensellerbiz&logNo=221494015560)

- 사용법
  [Tag Assistant Legacy (by Google)](https://chrome.google.com/webstore/detail/tag-assistant-legacy-by-g/kejbdjndbnbjgmefkgdddjlbokphdefk?hl=ko)

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>1. </li>
  <li>2. </li>
  <li>3. </li>
</ul>
</div>

#### 참고 영상

- [06. 구글 태그 매니저](https://youtu.be/tplvhWBGV_Q){% include video id="tplvhWBGV_Q" provider="youtube" %}
- [구글 애널리틱스4 (GA4) 강의 5. 이벤트 : GA4 GTM 이벤트 태깅하기. 플러스제로](https://youtu.be/hWrmkJZt1Sk){% include video id="hWrmkJZt1Sk" provider="youtube" %}

#### 참조 문서 및 사이트

- [데이터 영역](https://developers.google.com/tag-platform/tag-manager/web/datalayer)
- [구글 태그 매니저(google tag manager) vs gtag.js](https://www.datachef.co.kr/post_ga_tip/?idx=7438407&bmode=view)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
