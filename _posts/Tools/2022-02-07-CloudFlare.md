---
layout: single
title: "Cloudflare"
categories: Tools
tag: [Cloudflare, CDN, edge]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# Cloudflare란

## CDN edge server란 무엇인가?

[CDN](https://www.cloudflare.com/learning/cdn/what-is-a-cdn/) edge(에지) 서버는 네트워크 의 논리적 극단 또는 "[edge](https://www.cloudflare.com/learning/serverless/glossary/what-is-edge-computing/)"에 존재하는 컴퓨터입니다. 에지 서버는 종종 개별 네트워크 간의 연결 역할을 합니다. CDN 에지 서버의 주요 목적은 콘텐츠를 요청하는 클라이언트 시스템에 최대한 가깝게 저장하여 대기 시간 을 줄이고 페이지 로드 시간을 개선하는 것입니다.

에지 서버는 네트워크에 진입점을 제공하는 에지 장치 유형입니다. 다른 에지 장치에는 라우터와 라우팅 스위치가 있습니다. 에지 장치는 종종 다른 네트워크가 연결하고 전송을 공유할 수 있도록 인터넷 교환 지점(IxP) 내부에 배치됩니다.

### 에지 서버는 어떻게 작동할까?

특정 네트워크 레이아웃에서 여러 장치가 미리 정의된 하나 이상의 네트워크 패턴을 사용하여 서로 연결됩니다. 네트워크가 다른 네트워크나 더 큰 인터넷에 연결하려는 경우 트래픽이 한 위치에서 다른 위치로 흐르도록 하려면 일종의 브리지가 있어야 합니다. 네트워크 에지에서 이 브리지를 생성하는 하드웨어 장치를 에지 장치라고 합니다.

#### 네트워크는 에지에서 연결됩니다.

많은 장치가 연결된 일반적인 가정 또는 사무실 네트워크에서 휴대폰이나 컴퓨터와 같은 장치는 허브 앤 스포크 네트워크 모델을 통해 네트워크에 연결 및 연결 해제됩니다. 모든 장치는 동일한 LAN(Local Area Network) 내에 존재하며 각 장치는 중앙 라우터에 연결되어 서로 연결할 수 있습니다.

두 번째 네트워크를 첫 번째 네트워크에 연결하려면 어느 시점에서 네트워크 간에 연결이 이루어져야 합니다. 네트워크가 서로 연결할 수 있는 장치는 정의상 에지 장치입니다.

<img src="/assets/images/Tools/cdn-edge-network-device.png" />

이제 네트워크 A 내부의 컴퓨터가 네트워크 B 내부의 컴퓨터에 연결해야 하는 경우 연결은 네트워크 A에서 네트워크 에지를 거쳐 두 번째 네트워크로 전달되어야 합니다. 이 동일한 패러다임은 인터넷을 통해 연결될 때와 같이 보다 복잡한 컨텍스트에서도 작동합니다. 네트워크가 전송을 공유할 수 있는 기능은 네트워크 간 에지 장치의 가용성으로 인해 병목 현상이 발생합니다.

연결이 인터넷을 통과해야 하는 경우 네트워크 A와 네트워크 B 간에 더 많은 중개 단계를 수행해야 합니다. 간단하게 하기 위해 각 네트워크가 원이고 원이 접하는 위치가 네트워크의 가장자리라고 가정하겠습니다. 회로망. 인터넷을 통해 연결을 이동하기 위해 일반적으로 많은 네트워크와 연결되고 많은 네트워크 에지 노드를 가로질러 이동합니다. 일반적으로 연결해야 하는 거리가 멀수록 통과해야 하는 네트워크의 수도 많아집니다. 연결은 대상에 도달하기 전에 다른 인터넷 서비스 공급자와 인터넷 백본 인프라 하드웨어를 통과할 수 있습니다.

<img src="/assets/images/Tools/cdn-edge-server-placement.png" />

CDN 공급자는 여러 위치에 서버를 배치하지만 가장 중요한 일부는 서로 다른 네트워크 사이의 가장자리에 있는 연결 지점입니다. 이러한 에지 서버는 서로 다른 여러 네트워크와 연결되어 네트워크 간에 빠르고 효율적으로 트래픽을 전달할 수 있습니다. CDN이 없으면 전송은 출발지와 목적지 사이에 더 느리고/또는 더 복잡한 경로를 취할 수 있습니다. 최악의 시나리오에서 트래픽은 먼 거리를 "트롬본"합니다. 길 건너에서 다른 장치에 연결할 때 연결이 전국을 가로질러 다시 이동할 수 있습니다. 에지 서버를 주요 위치에 배치함으로써 CDN은 다른 네트워크 내부의 사용자에게 콘텐츠를 신속하게 전달할 수 있습니다. CDN 사용의 개선 사항에 대해 자세히 알아보려면 [CDN 성능 작동 방식](https://www.cloudflare.com/ko-kr/learning/cdn/performance/)을 살펴 보세요.

### 에지 서버와 원본 서버의 차이점은 무엇입니까?

[오리진 서버](https://www.cloudflare.com/ko-kr/learning/cdn/glossary/origin-server/)는 웹 속성이 CDN을 사용하지 않을 때 모든 인터넷 트래픽을 수신하는 웹 서버입니다. CDN 없이 원본 서버를 사용한다는 것은 각 인터넷 요청이 세계 어디에 있든 상관없이 원본 서버의 물리적 위치로 반환되어야 함을 의미합니다. 이렇게 하면 서버가 요청하는 클라이언트 시스템에서 멀어지는 만큼 로드 시간이 늘어납니다.

CDN 에지 서버 는 하나 이상의 원본 서버의 부하를 줄이기 위해 전략적 위치에 콘텐츠를 저장([캐시](https://www.cloudflare.com/ko-kr/learning/cdn/what-is-caching/))합니다. 이미지, HTML 및 JavaScript 파일(및 잠재적으로 다른 콘텐츠)과 같은 정적 자산(assets)을 요청하는 클라이언트 시스템에 최대한 가깝게 이동함으로써 에지 서버 캐시는 웹 리소스가 로드되는 데 걸리는 시간을 줄일 수 있습니다. 원본 서버는 CDN을 사용할 때 여전히 중요한 기능을 가지고 있습니다. 인증에 사용되는 해시된 클라이언트 자격 증명의 데이터베이스와 같은 중요한 [서버 측](https://www.cloudflare.com/ko-kr/learning/serverless/glossary/client-side-vs-server-side/) 코드가 일반적으로 원본에서 유지되기 때문입니다. 전 세계에 에지 서버 가 있는 [Cloudflare CDN](https://www.cloudflare.com/ko-kr/cdn/)에 대해 알아보십시오.

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

- [What is a CDN edge server?](https://www.cloudflare.com/de-de/learning/cdn/glossary/edge-server/)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
