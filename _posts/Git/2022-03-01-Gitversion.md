---
layout: single
title: "Gitversion, Semantic Versioning Specification (SemVer)"
categories: Git
tag: [Git, Version, SemVer]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# Semantic Versioning(SemVer)이란?

```json
"devDependencies": {
        "eslint": "8.11.0",
}
```

우리는 흔히 npm packages에서 위의 예시와 같이 버전이 일괄되게 표시되어있음을 알 수 있다. 이는 Github의 공동창업자인 톰 프레스턴 베르너(Tom Preston-Werner)가 만들었으며, 오픈소스 프로젝트에 일반적으로 사용되어 사용자가 이 package (api)가 어떤 식으로 변경되었는지가를 알 수 있다. 혹은 오픈소스가 아니더라도 개발자의 release 버전을 위와 같이 표기하면 좋기도 하다.

##

MAJOR Version: 기존 api가 변경 / 삭제 되었기 때문에 update 하면 동작하지 않을 수 있다는 경고의 의미
MINOR Version: 이전 버전과 호환되는 방식으로 API가 추가되었으니 살펴보라는 의미
PATCH Version: 이전 버전과 호환되는 버그 수정을 했을 경우

##

SemVer(유의적버전)을 쓰는 소프트웨어는 반드시 공개 API를 선언한다. 코드자체로 선언하거나, 문서로 엄격하게 명시해야 한다. (책임감 있는 개발자..)
Normal Version은 반드시 X.Y.Z 형태이며 음수가 아닌 정수여야 하며 절대 앞에 0이 붙으면 안되고 각 수는 증가하는 수여야 한다.
배포하면 그 버전의 내용은 절대 변경해서는 안된다. 😱
0(0.y.z)은 초기 개발을 위해서 쓴다. 아무 때나 마음대로 바꿀 수 있다.
1.0.0 버전은 공개 API를 정의한다. 이후 버전은 배포한 공개 API에서 어떻게 바뀌었는지에 따라 올린다.
MAJOR Version이 올라가면 MINOR Version과 PATCH Version은 0이 되야하고
MINOR Version이 올라가면 PATCH Version이 0이 반드시 되어야 한다.
정식 배포를 앞둔 pre-release version은 PATCH Version 바로 뒤에 붙임표(-)와 마침표(.)로 구분된 식별자를 더해서 표시할 수 있다. 식별자는 반드시 아스키(ASCII) 문자, 숫자, 붙임표로만 구성한다[0-9A-Za-z-]. 식별자는 반드시 한 글자 이상으로 한다. 숫자 식별자의 경우 절대 앞에 0을 붙인 숫자로 표기하지 않는다.
예) 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7, 1.0.0-x.7.z.92.
우선순위는 1.0.0-alpha < 1.0.0.
Build metadata는 수버전이나 정식배포 전 식별자 뒤에 더하기(+) 기호를 붙인 뒤에 마침표로 구분된 식별자를 덧붙여서 표현할 수 있다.
Build metadata.. Build metadata.. ??🧐가 무엇일까?
git commit 후 생기는 난수가 붙는 경우가 있는데 그 상태로 그대로 배포하는 경우 build metadata가 그것이였다.
예) 1.0.0-alpha+001, 1.0.0+20130313144700, 1.0.0-beta+exp.sha.5114f85.

<img src="/assets/images/Git/semver.png" />

```json
package.json
"Dependencies": {
  "react": "17.0.2",
}
```

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

- [유의적 버전 2.0.0-ko2](https://semver.org/lang/ko/)
- [Semantic Versioning - MAJOR, MINOR, PATCH와 명세에 관하여](https://velog.io/@slaslaya/Semantic-Versioning-2.0.0-MAJOR-MINOR-PATCH%EC%99%80-%EB%AA%85%EC%84%B8%EC%97%90-%EA%B4%80%ED%95%98%EC%97%AC)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
