---
layout: single
title: "모바일 기기로 테스트 및 디버깅하기"
categories: Test
tag: [Test, 테스트, 모바일, localhost, 디버깅, debugging]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# 모바일 테스트

웹이나 SPA 개발하기 위해서는 모바일로 테스트는 필수인데, 보통은 모바일 웹뷰를 테스트하기 위해서 크롬이나 파이어폭스로 모바일 웹뷰로 확인하는데 간혹 어떠한 문제들은 실제 모바일 환경에서만 발생하기도 한다. 이러한 문제들은 `cross browser testing`이나 `Browserstack` 툴들에도 확인되지 않기 때문에 실제 모바일 환경에서 확인해야하만 한다. 다음은 실질적인 모바일 환경에서 테스트하는 방법을 서술해보았다.

# 1. 같은 아이피 주소로 localhost 테스트하기

<img src="/assets/images/Test/ipv4.png" />

배포 및 개발시 보통 릴리즈하기 전에 `develop` 브랜치를 기반으로 하는 테스트 서버를 따로 두고는 한다. 그럼 localhost를 모바일 환경에서 테스트 어떻게 할까? 비교적 손쉽게 테스트할 수 있는데, 바로 데스크탑과 모바일 모두 같은 아이피를 맞춰주고, 데스크탑으로 localhost 실행시켜준 다음, 모바일로`IPv4`주소를 입력한 다음 localhost 주소를 입력해준다. 예를 들어 IPv4주소가 `192.160.0.123`이라고 가정한다면 `192.16.0.123:3000` 모바일에서 입력하면 확인 가능하다(`localhost:3000` 실행을 원할시)

[How to see your Localhost Website on your Mobile phone](https://youtu.be/ZqNxk5tiiQQ){% include video id="ZqNxk5tiiQQ" provider="youtube" %}

# 2.실제 핸드폰으로 Chrome Reomte 디버깅

만약 테스트 뿐만 아니라 Chrome Debugging을 하고 싶다면 USB 케이블로 핸드폰과 데스크탑을 연결시켜준 다음, 아래의 영상과 같이 진행하면 실제 모바일 환경에서 Debugging이 가능하다

[DevTools for Android? 🤔 Setting up Chrome Remote Debugging](https://youtu.be/5t5XZKUgp9Y){% include video id="5t5XZKUgp9Y" provider="youtube" %}

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>localhost를 테스트하려고 한다면 아이피 주소를 맞춰준다. </li>
  <li>디버깅을 하려면 케이블로 모바일과 데스크탑을 연결해준 다음 개발자 모드로 USB Debugging 옵션을 켜준 다음 디버깅을 한다 </li>
</ul>
</div>

#### 참조 문서 및 사이트

- [[Dev 개발] 모바일에서 로컬 열기 / 모바일에서 localhost 접속하기](https://anerim.tistory.com/164)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
