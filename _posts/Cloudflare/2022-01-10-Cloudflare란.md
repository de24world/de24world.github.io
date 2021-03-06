---
layout: single
title: "Cloudflare란"
categories: Cloudflare
tag: [Cloudflare, CDN, edge, 클라우드플레어, static content]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# Cloudflare란

[What is Cloudflare?](https://youtu.be/XHvmX3FhTwU){% include video id="XHvmX3FhTwU" provider="youtube" %}

공식 홈페이지에 따르면 `Cloudflare는 웹사이트, API, 응용 프로그램 등 외부로 열려 있는 자원을 보호하고 안정성을 보장합니다. 방화벽 뒤의 응용 프로그램, 팀, 장치 같은 내부 리소스를 보호합니다. 또한, 전 세계로 확장할 수 있는 응용 프로그램을 개발하기 위한 플랫폼입니다` 라고 정의하고 있다. 제공하는 서비스로는 `CDN, *DNS, DDoS방어, 부하 분산, 속도 제한, WAF, API보호` 등 여러가지 서비스를 제공하고 있다.

- [DNS에 관한 설명 영상](https://youtu.be/6fc9NAQkcv0)

<img src="/assets/images/Cloudflare/cloudflare.png" />

많은 서비스와 용어들이 등장하기 때문에 어려울 수 있는데, 쉽게 말해 `다리` 역할을 한다고 보면 이해하기 쉽다. 한국 사용자가 미국에 서버를 두고 있는 미국 온라인 쇼핑몰을 사용한다고 가정해보자. 그럼 한국에서 미국까지 HTTP 요청(Request)이 이루어져야하며 HTML, CSS, JS, 이미지 파일 등 응답받기까지 비교적 시간이 오래 걸린다.

하지만 Cloudflare는 전세계 여러 국가에 자체 서버를 두고 있어 미국까지 가지 않고, JS, CSS, 이미지 파일 등 `정적 컨텐츠(static content)`를 중간에 Cloudflare를 거쳐(동적 컨텐츠 포함) 한국 근처의 서버로 요청하고 응답받게 되어 비교적 빠르다고 할 수 있다. 이를 `CDN(Content Delivery Network)`라고 한다. 또한 악성 트래핑 필터링, DDoS 완화 작업 등도 할 수 있어 서버 부하를 줄이는 역할까지 한다.

## 클라우드플레어의 장점

- CDN을 별도로 설정해줄 필요 없이 네임서버 설정 변경만으로 모든 컨텐츠를 CDN을 통해 전달이 가능하다.

  - 파일 확장자들을 기준으로 정적인 컨텐츠들은 origin에서 한번만 로드한 후 캐시해서 자동으로 CDN처럼 동작한다 (커스텀하게 규칙을 설정이 가능하다.) HTML은 캐싱하지 않는다.
  - 안타깝게도 동적인 컨텐츠의 주소들만 따로 분류해서 클라우드 플레어를 거치지 않도록 따로 설정하는것은 불가능하다.

- 클라우드플레어 서버를 거칠때 악성 트래픽 필터링, DDoS 완화 등의 작업을 할 수 있게되어 실제 서버로 들어오는 부하를 많이 줄일 수 있다. 예를들어 의심되는 트래픽에 대해서 자동입력 방지 문자 등을 보여주고 이 부분을 통과할 경우에만 정상적으로 요청을 처리해 준다던가 하는 식으로 중간 차단을 해준다.

- 실제 서버는 클라우드플레어 서버의 뒤쪽으로 숨겨져있기 때문에 IP를 완전히 숨길 수 있어서 추가적인 보안상의 이점이 있다.

- 일반적으로 생각했을때 동적인 컨텐츠의 경우 캐시가 불가능하기 때문에 직접 서버로 연결하지 않고 클라우드플레어 서버를 한번 거쳐서 오게되면 속도가 더 느려질 것으로 보인다. 하지만 클라우드플레어가 전세계에 운영중인 Edge들과 해당 Edge들을 이어둔 전용 네트워크 회선을 사용하면, 실제 인터넷 상에서 엔드투엔드(End-to-End)로 가기위해 거쳐야 할 “hops” 수가 훨씬 줄어든다고 클라우드플레어 측에서 설명 하고 있다. 이 부분은 네트웍 상황에따라 장점이 될 수도있고 단점이 될 수도 있는 부분이라 자신의 상황에 맞게 사용해야 할 것 같다. (특히 한국의 경우 엔터프라이즈 유저가 아니면 한국 Edge 사용 불가하기 때문에 국내 사용자들이 접속시에 오히려 속도가 더 느려질 수도 있으니 주의해야 한다.)

## 클라우드플레어의 단점

- 정적인 컨텐츠 경우에는 일반적인 CDN과 동일하게 속도가 매우 빠르지만, 동적인 컨텐츠의 경우 클라우드플레어서버를 통해 실제 서버(origin) 에서 컨텐츠를 가져와야 한다. 앞서 장점쪽에서 언급했듯이 네트워크 환경에따라 이 부분이 더 빠를때도 있지만 항상 그렇다는것을 보장 할수 없다. 때문에 페이지가 열리는 속도와 직결되는 TTFB(Time To First Byte)가 느려질 가능성이 충분히 존재하고, TTFB가 느려질수록 구글 등의 검색엔진의 SEO에서 페널티를 받을 가능성도 있기때문에 주의해서 사용해야 한다.

- 서버로 들어오는 모든 요청이 클라우드플레어를 통해서 전달되기때문에 정확한 액세스 로그기록이 힘들어진다. 때문에 특정 사용자의 기록을 정확히 찾아내서 문제점을 파악한다거나 할 때 좀더 어려움을 겪을 수 있다.

- 웹이 클라우드플레어에 의존적이게 되는데, 2019년에 클라우드 플레어가 18분 정도 서버 다운된적이 있어, Cloudflare를 사용하고 있는 전세계의 많은 웹들이 다운된 적이 있다.

## 클라우드 플레어 타사 서비스와 비교

[cloudflare pages vs firebase](https://bejamas.io/compare/cloudflare-pages-vs-firebase/)

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>글로벌 서비스를 사용하는 웹(앱)이라면 CDN 사용을 고려해보자 </li>
  <li>트래픽이 많은 웹도 트래픽 필터링 서비스나 DDoS 완화 등 서버부하를 Cloudflare 통해서 줄일 수 있다. 보안 문제에 있어서 굉장히 유용한 것 같다</li>
  <li>국내 호스팅 또는 도메인 등록 대행 업체들이 제공하는 네임서버(RTT 200ms 내외)이 비해 훨씬 안정적이고 속도가 빠르니 Cloudflare 네임서버로만 사용해도 괜찮을 것 같다</li>
  <li>한국으로만 대상하는 비교적 규모가 적은 웹의 경우 굳이 Cloudflare가 필요할까 싶다. Input 대비 Output이 크지 않을듯 싶다</li>

</ul>
</div>

#### 참조 문서 및 사이트

- [클라우드플레어(Cloudflare) 동작 원리](https://www.letmecompile.com/how-cloudflare-works/)
- [클라우드플레어(Cloudflare) 서비스 문서](https://developers.cloudflare.com/)
- [클라우드 플레어 강좌](https://egghead.io/q?q=cloudflare)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
