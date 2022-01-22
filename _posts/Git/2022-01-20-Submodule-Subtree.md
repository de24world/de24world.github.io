---
layout: single
title: "서브모듈(submodule)와 서브트리(subtree)"
categories: Git
tag:
  [Git, Submodule, 서브모듈, Repository, 레지포토리, 저장소, Subtree, 서브트리]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# 서브모듈(Submodule)이란?

<img src="/assets/images/Git/submodules-monorepo.png" />

서브모듈이란, 말 그대로 저장소 안에 또 다른 별개의 저장소를 의미하는 서브 저장소(모듈?)이라고 보면 된다. 보통 프로젝트를 진행하다보면 여러 가지 저장소(repository) 운영하기 마련인데, 이때 공통으로 사용하는 코드나 라이브러리를 별도의 저장소 즉, 서브모듈로 두어 관리하면 관리가 용이해진다.

## 서브모듈 사용방법

1. 우선 메인 저장소에 <strong>`git submodule add (서브모듈 Git URL) + (추가하고 싶은 폴더, 예:lib)`</strong> 명령어로 서브모듈을 추가해준다.

```
$ git submodule add https://github.com/de24world/submoduleRepoExample.git .libs
Cloning into '.libs/submoduleRepoExample'...
remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 0), reused 11 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.
```

2. 그럼 `.libs`이라는 폴더와 `.gitmodules`라는 파일이 생성된다. `.libs`이라는 폴더안에는 `https://github.com/de24world/submoduleRepoExample.git`의 저장소의 폴더 및 파일들이 불러와져 있고 `.gitmodules`에는 서브모듈에 대한 정보(경로 및 url)이 나와있다.

```
.gitmodules
[submodule ".libs"]
    path = libs
    url = https://github.com/de24world/submoduleRepoExample.git
```

3. 만약 메인저장소에 `.libs`의 저장소에서 변경사항이 있고, 이 변경사항을 메인저장소의 submodule(.libs)에 반영하고 싶다면 `git submodule update --remote`라고 명령어를 입력해주면 `.gitmodules`에 있는 모든 submodule 원격저장소의 변경사항을 업데이트해준다. <strong>(--remote 없이 입력하면 원격저장소의 최신 상태가 아닌 commit한 상태의 버전의 최신상태로 업데이트된다)</strong>

## 서브모듈 명령어

```
[] 안의 표시는 생략 가능, 중요
git submodule [--quiet] [--cached]
: 현재 서브모듈을 보여준다.

git submodule [--quiet] add [<options>] [--] <repository> [<path>]
: 서브모듈을 추가해준다.

git submodule [--quiet] status [--cached] [--recursive] [--] [<path>…​]
: 서브모듈의 상태를 확인해준다.

git submodule [--quiet] init [--] [<path>…​]
: 서브모듈 정보를 기반으로 로컬 환경설정 파일을 만들어준다. 즉 모든 서브모듈을 가져온다.

git submodule [--quiet] deinit [-f|--force] (--all|[--] <path>…​)
: 서브 모듈 등록을 해제해준다.

git submodule [--quiet] update [<options>] [--] [<path>…​]
: 서브모듈의 리모트 저장소에서 데이터를 가져오고 Checkout한다.

git submodule [--quiet] set-branch [<options>] [--] <path>

git submodule [--quiet] set-url [--] <path> <newurl>

git submodule [--quiet] summary [<options>] [--] [<path>…​]
: 커밋(commit)하지 서브 모듈의 상태를 보여준다.

git submodule [--quiet] foreach [--recursive] <command>
: 서브모듈들이 여러개가 있을 때 여러 서브모듈에서 한 번에 실행할 수 있다.

git submodule [--quiet] sync [--recursive] [--] [<path>…​]

git submodule [--quiet] absorbgitdirs [--] [<path>…​]
```

- recursive는 서브모듈의 하위의 모든 내용까지 포함(예 : 서브모듈 안에 또 다른 서브모듈이 있을 수도 있음)

# 서브트리(Subtree)란?

<img src="/assets/images/Git/subtree.png" />

# 서브모듈 vs Subtree

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>1. </li>
  <li>2. </li>
  <li>3. </li>
</ul>
</div>

#### 참고 영상

- [저장소 안에 저장소 - git submodule](https://youtu.be/TAe4uZqYt6c){% include video id="TAe4uZqYt6c" provider="youtube" %}

#### 참조 문서 및 사이트

- [7.11 Git 도구 - 서브모듈](https://git-scm.com/book/ko/v2/Git-%EB%8F%84%EA%B5%AC-%EC%84%9C%EB%B8%8C%EB%AA%A8%EB%93%88)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}

```

```
