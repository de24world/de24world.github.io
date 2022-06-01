---
layout: single
title: "해킹 공부 자료"
categories: Hacking
tag: [Hacking, backend, sample]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# 칼리리눅스

[칼리 리눅스 설치 과정 ① / Kali Linux installation process ①](https://information-security-vlog.tistory.com/4)

- [칼리리눅스 한글 폰트 설치와 한글 입력기 설정, 한글을 자유롭게 사용~](https://youtu.be/zv9ClOSixls){% include video id="zv9ClOSixls" provider="youtube" %}

- [칼리리눅스 VPN 사용법](https://youtu.be/dbicbkM0Xrg){% include video id="dbicbkM0Xrg" provider="youtube" %}

terminal에서 `xset b off` 혹은 `sudo rmmod pcspkr` rmmod는 모듈을 제거하는 명령어이고, pcspkr은 스피커 모듈이다. (해당 방법은 일시적인 방법, 영구적 방법 현재 필자의 칼리리눅스에 적용 안됨)

## 정보 수집을 위한 칼리리눅스 (Tool = 명령어)

`whois ...(url)` : 해당 URL의 도메인 이름, IP주소, 인터넷 자원의 소유자와 범위 등 `도메인 등록된 정보를 알려준다`.
알려준다.

`host ...(url)` : 해당 URL의 `호스트 정보`를 알려준다

`fierce` : 대상에서 `사용하는 모든 IP주소와 호스트를 찾아 사전공격, 근접 네트워크 스캔과 일반적으로 기존 DNS 도구에서 사용되는 도메인 이름에 대한 검색, sone transfer, soa 레코드 덤프를 시도.`

`theharvester` : theharvester는 검색 엔진, PGP 키 서버 및 shodan 컴퓨터 데이터베이스와 같은 다양한 공공 데이터 소스에서 `이메일, 이름, 하위 도메인, IP 및 URL 정보`를 수집하는데 사용하는 도구 입니다.

`nmap` : `서버 포트(Port)를 스캔`해준다.

`whatwep` : 웹사이트를 식별하고, 콘텐츠 관리 시스템, 블로그 플랫폼, 통계 분석 패키지, 자바 스크립트 라이브러리, 웹서버와 임베디드 장치 등의 `웹 기술을 인식`한다.

## 공격을 위한 칼리리눅스 (Tool = 명령어)

### sqlmap

예 ) 로그인시 URL Parameter에 ID나 Password와 같이 값이 있으면 공격하여 유저들의 아이디 및 비밀번호 정보를 탈취할 수 있다

[간단한 실습을 통한 sqlmap 사용법](https://koromoon.blogspot.com/2020/07/sqlmap.html)
[sqlmap 사용법](https://jdh5202.tistory.com/648)

[[화이트해커][웹모의해킹] 45강. SQL인젝션 공격 실습: SQLMAP 자동화 공격](https://youtu.be/5ncZimbfgLQ){% include video id="5ncZimbfgLQ" provider="youtube" %}

[3. SQLMAP - SQL Injection 확인 툴 [칼리리눅스를 이용한 해킹소개]](https://youtu.be/yvaWpU2IRVs){% include video id="yvaWpU2IRVs" provider="youtube" %}

### 참조영상

[화이트해커][웹모의해킹] 9강. 웹 해킹 보안 실습용 웹 어플 DVWA 설치 : https://youtu.be/yWwlO0wuNac

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

- []()

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
