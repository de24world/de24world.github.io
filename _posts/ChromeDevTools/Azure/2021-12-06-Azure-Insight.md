---
layout: single
title: "Application Insights, Azure 모니터링"
categories: Azure
tag: [Azure, Monitoring, APM]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# Application Insights란?

Application Insights는 어플리케이션 성능 관리 서비스([APM, Application Performance Management](https://ko.wikipedia.org/wiki/%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98_%EC%84%B1%EB%8A%A5_%EA%B4%80%EB%A6%AC))로, 어플리케이션을 모니터링한다. [Azure Monitor](https://docs.microsoft.com/ko-kr/azure/azure-monitor/overview) 기능으로 , 성능(Performance) 이상을 자동으로 감지하고, 문제를 진단하고 사용자가 실제로 앱을 사용하여 수행하는 작업을 파악할 수 있는 강력한 분석 도구를 포함하고 있습니다. 성능 및 가용성을 지속적으로 향상시킬 수 있도록 설계되었습니다. 온-프레미스, 하이브리드 또는 퍼블릭 클라우드에서 호스팅되는 .NET, Node.js, Java 및 Python을 포함하여 다양한 플랫폼의 앱에서 작동합니다. DevOps 프로세스와 통합되며, 다양한 개발 도구와의 연결 지점을 갖고 있습니다. Visual Studio App Center를 통합하여 모바일 앱에서 원격 분석을 모니터링하고 분석할 수 있습니다.

## Application Insights의 작동 방식

<img src="/assets/images/Azure/Application-Insights.png" />

## Application Insights는 무엇을 모니터링하나요?

Application Insights는 애플리케이션 팀에서 앱의 작동 방식과 사용 방식을 이해하는 데 도움을 주기 위해 고안되었습니다. 다음 사항을 모니터링합니다.

- 요청 속도, 응답 시간 및 실패율 - 하루 중 어느 시간에 어떤 페이지를 가장 많이 방문하는지, 사용자가 어디에 있는지 확인합니다. 어떤 페이지가 가장 성능이 우수한지 확인합니다. 요청이 더 있는데 응답 시간과 실패율이 높아지면 아마도 리소스 문제가 있는 것입니다.
- 종속성 비율, 응답 시간 및 실패율 - 외부 서비스 때문에 속도가 느려지는지 확인합니다.
- 예외 - 집계된 통계를 분석하거나 특정 인스턴스를 선택하여 스택 추적 및 관련 요청을 자세히 분석합니다. 서버 및 브라우저 예외가 전부 보고됩니다.
- 페이지 보기 및 로드 성능 - 사용자의 브라우저에서 보고합니다.
- 웹 페이지의 AJAX 호출 - 속도, 응답 시간 및 실패율.
- 사용자 및 세션 수.
- Windows 또는 Linux 서버 컴퓨터의 성능 카운터 - CPU, 메모리, 네트워크 사용량 등.
- Docker 또는 Azure의 호스트 진단.
- 앱의 진단 추적 로그 - 추적 이벤트를 요청과 상호 연결하는 데 사용됩니다.
- 판매된 품목, 승리한 게임 등의 비즈니스 이벤트를 추적하기 위해 개발자가 직접 클라이언트 또는 서버 코드로 작성하는 사용자 지정 이벤트 및 메트릭.

<div class="notice--success">
<h2>요약</h2>

<h3>라이브 애플리케이션을 모니터링</h3>

<h4>다양한 플랫폼의 앱에서 작동(.NET, Node.js, Java 및 Python)</h4>

<h3>다양한 요청에 대한 모니터링</h4>
<ul>
<li> 요청 속도, 응답 대기 시간 및 실패율 </li>
<li>  페이지 보기 및 로드 성능</li>
<li> 사용자 및 세션 로드 성능</li>
<li> 사용자 및 세션 로드 성능</li>
<li>  서버 성능 카운터</li>
<li> 사용자 지정 이벤트 및 메트릭</li>
</ul>
</div>

#### 참고 영상

- [[20분 Class] Azure 1 Day 정복하기 1편 - 핵심 Azure 서비스 살펴보기](https://youtu.be/aagsTCiQhyo){% include video id="aagsTCiQhyo" provider="youtube" %}
- [How to monitor app performance with Azure Monitor Application Insights
  ](https://youtu.be/paAYgjNITik){% include video id="paAYgjNITik" provider="youtube" %}

#### 참조 문서 및 사이트

- [Application Insights란?](https://docs.microsoft.com/ko-kr/azure/azure-monitor/app/app-insights-overview)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
