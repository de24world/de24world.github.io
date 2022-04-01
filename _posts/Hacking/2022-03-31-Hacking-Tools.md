---
layout: single
title: "Hacking Tools"
categories: Hacking
tag: [Hacking, Tools, sample]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

<img src="/assets/images/CLS/width_height.gif" />

## 정보수집(Information Gathering)

해킹에 앞서 Target에 대한 정보를 수집하는 것이 중요한데, 여러가지 Tools들을 이용하여 정보를 수집할 수 있다. 수집한 정보를 이용하여 Target의 취약점을 분석하고 공격할 수 있는 방법을 늘린다. 알아낼 수 있는 정보들로는 DNS 정보 수집, 네트워크 정보 수집, 호스트 정보 수집, OS 정보 수집, 서비스 목록화, 네트워크 범위 파악, 활성화된 머신 식벼, 개방 포트 탐색, 서비스 식별, `말테고(maltego)`를 이용한 위협 평가, 네트워크 매핑 등이 있다.

1. [Whois Look up](https://whois.domaintools.com/) - Find info about the owner of the target
   : 웹사이트의 도메인, IP 주소, 서버 타입 등의 정보를 알 수 있다.

2. [Netcraft Site Report](https://sitereport.netcraft.com/?url=) - Shows technologies used on the target

3. [Robtex DNS lookup](https://www.robtex.com/) - Shows comprehensive info about the target website.

4. [Maltego](https://www.maltego.com/product-features/) - Maltego is an information gathering tool that can be used to collect information about anything. To run maltego type the follwing in terminal `maltegoce`

[Maltego 설치방법 in KaliLinux](https://installati.one/kalilinux/maltego/)

### 같은 서버를 쓰는 웹사이트들 알아내기

### Subdomain 알아내는 법

칼리리눅스에서 `knockpy + url` 치면 Subdomain(예:mail.google.com) 등을 알아낼 수 있다.

## 공격 툴

1. [exploit-db](https://www.exploit-db.com/)

- 프로그램, 운영체제, 데이터베이스, 전송 및 보안 장비/운영체제에 대한 취약점 분석 코드 제공
- Kali Linux에는 exploit-db에서 제공하는 취약점 코드드들이 내장되어 있음

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
