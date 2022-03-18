---
layout: single
title: "Cloudflare edge Server"
categories: Cloudflare
tag: [Cloudflare, CDN, edge]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# Cloudflare Workers란

Workers는 Cloudflare사의 서버리스(Serverless) 컴퓨팅 서비스로, 전세계의 수많은 Cloudflare Edge 네트워크를 통해 빠른 반응속도로 응답할 수 있는 매력적인 서비스다.

<img src="/assets/images/Cloudflare/cloudflare-workers.png" />

## Serverless (컴퓨팅)란?

서버리스 컴퓨팅은 특정 서버에 코드를 올려놓고 요청을 처리하는 것이 아니라, 말 그대로 어떤 서버에 종속되지 않은(serverless) 코드를 배포하여 필요할 때마다 요청을 처리하는 기술이다.

기존의 서버-종속적인 컴퓨팅 모델과 비교해 서버리스 컴퓨팅은 다음과 같은 이점을 가진다.

- 비용 절감: 대부분의 서버리스 서비스는 해당 코드가 ‘실제로 사용한’ 자원(CPU, 메모리, 네트워크)에 대해서만 요금을 부과한다. 기존의 서버-종속적인 컴퓨팅 모델은 요청이 들어오지 않아도 해당 코드가 서버를 계속 점유하고 있어야 하지만, 서버리스 컴퓨팅의 경우에는 요청이 들어올 때만 대응되는 코드를 실행하고 남는 시간에는 다른 요청에 대해 코드를 실행하는 식으로 자원을 공유할 수 있기 때문에 운영사 입장에서는 쓴 만큼만 요금을 부과할 수 있다.

- 자동 스케일 조정: 특정 요청이 몰릴 때 더 많은 서버에서 같은 코드를 실행하도록 자동적으로 확장/축소할 수 있다.

- 개발 기간 단축: 대부분의 서버리스 서비스는 REST 엔드포인트처럼 동작하므로 HTTP 서버를 구성하거나 하는 시간적 비용을 줄일 수 있다. 또한 서버리스 코드는 태생적으로 ‘stateless’하기도 하므로(하지만 workers에서는 stateless가 아니긴 하다. :P) 프로그래머는 로직과 상태를 분리할 수 있게 된다

## Cloudflare Workers 타사(AWS Lambda) 비교 장점

- 타사에 비해 폭넓은 에지 수: Cloudflare의 데이터센터가 더 많으니 전세계 범위에서 평균적인 레이턴시가 더 적다고 주장한다. (자기 나라에 있을 확률이 높으니까)

- Cold start 없음: 타사 서비스는 일정 시간동안 코드가 실행되지 않으면 다음의 첫 실행이 오래 걸리는데 Workers의 경우 이러한 문제가 없다고 한다.

- Rust 공식 지원
<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>1. </li>
  <li>2. </li>
  <li>3. </li>
</ul>
</div>

#### 참고 영상

- [How Cloudflare Workers delivers serverless computing](https://youtu.be/42E8DWdZgYc){% include video id="42E8DWdZgYc" provider="youtube" %}

#### 참조 문서 및 사이트

- [Cloudflare Workers Rust SDK 사용기](https://blog.cro.sh/posts/cloudflare-workers-rust/)
- [Cloudflare Workers — 서버리스](https://bbirec.medium.com/cloudflare-workers-%EC%84%9C%EB%B2%84%EB%A6%AC%EC%8A%A4-4de0d9d6aeb2)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
