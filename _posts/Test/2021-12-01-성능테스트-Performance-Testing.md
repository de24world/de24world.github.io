---
layout: single
title: "성능 테스트(Performance Testing)"
categories: Web
tag: [
    성능테스트,
    Performance Testing,
    서버 부하 테스트,
    Lasttest,
    load testing,
    하중시험,
    트래픽 테스트,
    Browser Test,
    Protocol Test,
    Stress Testing,
    최고점 부하 테스트
    Spike Testing,
    내구성 테스트,
    Stability Testing,
  ]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

테스트에는 굉장히 종류가 많은데, 오늘은 소프트웨어가 사용자 시스템에서 어떻게 작동하는지 확인하기 위한 **성능테스트(Performance Testing)** 종류에 대해서 정리해보았다.

# 성능 테스트란?

보편적으로 알려진 성능 테스트는 '다중 사용자 환경에서 네트쿼으 트래픽이 요구되는 상황에서 처리 능력을 평가하기 위한 테스트'라고 할 수 있다. 웹에서는 여러명의 동시 사용자를 발생시켜 성능을 체크를 하게 된다.

# 성능 테스트가 필요한 이우

- 소프트웨어(어플리케이션 등) 성능 요건을 충족하는 판별(예를 들어 시스템은 최대 1000명의 동시 사용자를 처리해야함)
- 애플리케이션 내 컴퓨터 **병목 현상**(Bottlenecks, 병의 목처럼 넓은 길이 갑자기 좁아짐으로써 나타나는 교통 정체 현상으로 컴퓨터 성능 저하 현상을 말한다) 유발하는지 위치 파악
- 두 개 이상의 시스템 비교 및 가장 성능이 좋은 시스템 식별
- 최대 트래픽 이벤트에서 안정성 측정

<img src="/assets/images/Test/performance_testing.png" />

# 성능 테스트 종류

## 1. 부하 테스트(Load Testing, 독일어로는 Lasttest)

- 일정 시간 동안 부하를 가하여 서버가 처리할 수 있는 최대 TPS(Transaction Per Second, 1초에 시스템이 처리할 수 있는 트랜잭션의 수)와 응답시간을 산출(가장 일반적인 성능 테스트). 여기서 부하를 가한다는 것은, 동시단말사용자(concurrent users)와 트랜잭션을 증가시키면서 테스트 중이 애플리케이션의 동작을 확인하는 것을 의미함으로써, 'Endurance testing' 또는 'Volume testing`이라고 부를 수도 있습니다. Load Testing의 주요 목적은 과부하 상태(under heavy load)에서 시스템이 잘 작동될 때, 응답시간과 애플리케이션의 지구력(staying power)을 모니터링하는 것입니다. Load Testing과 아래에 기술된 테스트들은 모두 비기능 테스트(NFT/ Non Functional Testing)에 속하며, 소프트웨어 애플리케이션의 비기능 요구사항을 테스트하기 위해 설계되었습니다. Load Testing은 테스트중인 애플리케이션이 견딜 수 있는 부하의 양을 확인하기 위해 수행됩니다. ‘성공적으로 수행된 Load Testing’은 지정된 테스트 케이스가 할당된 시간동안 오류없이 수행된 경우에만 가능합니다.

## 2. 내구성 테스트(Endurance Test)

- 긴 시간동안 부하를 가하여 시스템의 안정성을 점검하는 것이 목적
- 일반적으로 최대 TPS가 나오는 가상 사용자만큼 부하를 가하는 상태를 지속

## 3. 스트레스 테스트(Stress Test)

- 정상보다 더 많은 부하를 주는 테스트. Stress Testing은 CPU, Memory, Disk Space 등과 같은 하드웨어 자원이 충분하지 않을 때, 소프트웨어의 안정성을 확인하는 Performance Testing의 한 유형입니다. Stress Testing의 기본 개념은 시스템의 오류를 확인하고, 어떻게 시스템이 정상적으로 복구되는지를 살펴보는 것입니다. Stress Testing은 시스템 하드웨어 자원에서 처리할 수 없는 많은 수의 동시단말사용자(concurrent users)/프로세스로 소프트웨어에 부하를 주는 Negative Testing입니다. 이 Testing은 피로시험(Fatigue testing)으로도 알려져 있습니다. Stress Testing의 기본 개념은 시스템의 장애를 확인하고 시스템이 어떻게 정상적으로 복구되는지를 주시하는 것입니다. 이러한 품질 특성을 회복성(recoverability)이라고 합니다.

## 4. 스파이크 테스트(Spike Test)

- 순간적으로 사용자 수를 증가시키는 테스트(수강신청 시스템 등). Spike testing은 Stress Testing의 Subset입니다. 테스트 대상 시스템에 대해, 상용 운영환경에서 예상되는 부하 이상의 Workload를 짧은 기간동안 반복적으로 증가시킬 때 나타나는 성능 특성을 검증하기 위해 수행합니다.

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>1. </li>
  <li>2. </li>
  <li>3. </li>
</ul>
</div>

#### 참고 영상

- [Github 블로그](https://youtu.be/13xMwTTkQ30){% include video id="13xMwTTkQ30" provider="youtube" %}

#### 참조 문서 및 사이트

- [소프트웨어 성능 테스트 요구 사항 및 필수 구성 요소](https://blog.naver.com/PostView.nhn?blogId=ki630808&logNo=222147614041)
- [성능테스트의 유형](https://softwareqalab.tistory.com/58)
- [SW 성능 테스트 실무의 이해 - 네이버 블로그](https://blog.naver.com/PostView.nhn?blogId=wisestone2007&logNo=222071631718&categoryNo=44&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=search)

- [웹 사이트 스트레스 테스트를위한 7 가지 성능 테스트 도구](https://www.webhostingsecretrevealed.net/ko/blog/web-tools/load-testing-tools/)
- [Flood Element 개발자 블로그](https://notes.nicolevanderhoeven.com/Fork+My+Brain)
- [Load Testing vs Stress Testing vs Performance Testing: Difference Discussed](https://www.guru99.com/performance-vs-load-vs-stress-testing.html)
- [Performance Testing vs. Load Testing vs. Stress Testing
  ](https://www.blazemeter.com/blog/performance-testing-vs-load-testing-vs-stress-testing)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
