---
layout: single
title: "Gitversion, Semantic Versioning Specification (SemVer)"
categories: Git
tag: [Git, Version, SemVer, 틸드, 캐럿]
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

우리는 흔히 npm packages에서 위의 예시와 같이 버전이 일괄되게 표시되어있음을 알 수 있다. 이는 Github의 공동창업자인 톰 프레스턴 베르너(Tom Preston-Werner)가 만들었으며, 오픈소스 프로젝트에 일반적으로 사용되어 사용자가 이 package (api)가 어떤 식으로 변경되었는지가를 알 수 있다. 혹은 오픈소스가 아니더라도 개발자의 release 버전을 위와 같이 표기하면 좋기도 하다. 즉, 시맨틱 버저닝(Semantic Versioning)이란, `소프트웨어의 버전 변경 규칙에 대한 제안`을 뜻한다.

## Major, Minor, Patch 버전

<img src="/assets/images/Git/semver.png" />

- MAJOR Version(`x`.y.z): 하위호환이 되지 않는 API변화들
- MINOR Version(x.`y`.z): 하위호환이 되는 범위내에서 기능 추가들
- PATCH Version(x.y.`z`): 하위호환이 되는 범위내에서 bug fix

## 규칙

- MAJOR Version이 올라가면 MINOR Version과 PATCH Version은 0이 되야합니다.
- MINOR Version이 올라가면 PATCH Version이 0이 반드시 되어야 합니다.
- 정식배포전에 pre-release하는 경우에는 -또는 . 을 사용합니다.
- 정식배포전에 git commit후 난수가 붙는 경우 그대로 배포할 경우를 build metadata라고 합니다.
  ex) 16.9.0-alpha.0
- MAJOR에 0으로 시작하는 경우(0.y.z)는 은 초기 개발을 위해서 사용합니다.

## 버전 범위

```
1.2.3
>1.2.3
>=1.2.3
<1.2.3
<=1.2.3
```

### 틸드(~)와 캐럿(^)

- 틸드(~): x.y.z 중 z 범위 내에서 버전 업데이트
- 캐럿(^): x.y.z 중 x 이하 하위호환성이 보장되는 범위 내에서 버전 업데이트

- ~1.2.3: `>=1.2.3 <1.3.0`
  틸드이고, 위의 정의에 따라서 z범위내에서 버젼 업데이트 한다.
  그러면 범위가 1.2.3을 포함해서 같거나 크고, 1.3.0보다 작은 범위내에서 업데이트 한다.
- ^1.2.3: `>=1.2.3 <2.0.0`
  캐럿은, 위의 정의에 따라 x이하 하위 호환성이 보장되는 범위내에서 버전 업데이트 한다.
  1.2.3보다 크거나 같고, 2.0.0보다 작은 범위내에서 업데이트 한다.
  결국 Major버전이 바뀌지 않고, 하위호환성을 유지하기 때문에 실무에서 가장 많이 사용한다!

### 틸드와 캐럿의 차이Permalink

- 틸드(~)는 현재 지정한 버전의 마지막 자리 내의 범위에서만 자동으로 업데이트합니다.
  ~0.0.1 : >= 0.0.1 < 0.1.0
  ~0.1.2 : >= 0.1.2 < 0.2.0

- 캐럿은 1.y.z 내에서는 하위호환성이 보장되므로 그 내에서는 모두 업데이트하겠다는 의미입니다.
  ^1 : >= 1.0.0 < 2.0.0
  ^1.1.2 : >= 1.1.2 < 2.0.0
  ^1.1 : >= 1.1.0 < 2.0.0

#### 참고 영상

- [Tilde(~) and Caret(^) symbol in package json](https://youtu.be/1a-71rzTmA0){% include video id="1a-71rzTmA0" provider="youtube" %}

#### 참조 문서 및 사이트

- [유의적 버전 2.0.0-ko2](https://semver.org/lang/ko/)
- [Semantic Versioning - MAJOR, MINOR, PATCH와 명세에 관하여](https://velog.io/@slaslaya/Semantic-Versioning-2.0.0-MAJOR-MINOR-PATCH%EC%99%80-%EB%AA%85%EC%84%B8%EC%97%90-%EA%B4%80%ED%95%98%EC%97%AC)
- [Semantic Versioning이란?](https://velog.io/@iamjoo/Semantic-Versioning%EC%9D%B4%EB%9E%80)
- [npm package.json의 verison과 틸드tilde(~)와 캐럿caret(^)](https://umanking.github.io/2022/05/05/npm-version-tilde-caret/)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
