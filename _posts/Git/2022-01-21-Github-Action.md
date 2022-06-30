---
layout: single
title: "Github Action"
categories: Git
tag: [Git, Action, Workflow, CI, CD, Jobs, Events, Actions, Runners]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# Github Actions 개요?

GitHub Actions는 빌드, 테스트 및 배포 파이프라인을 자동화할 수 있는 \*CI/CD(지속적 통합 및 지속적 전달) 플랫폼입니다. Repository에 대한 모든 pull request들을 빌드 및 테스트하거나 병합된 pull request들을 프로덕션에 배포하는 워크플로를 만들 수 있습니다.

[GitHub Actions - Supercharge your GitHub Flow](https://youtu.be/cP0I9w2coGU){% include video id="cP0I9w2coGU" provider="youtube" %}

## CI(Continuous Integration)/CD(Continuous Deployment)란?

CI/CD는 애플리케이션 개발 단계를 자동화하여 애플리케이션을 보다 짧은 주기로 고객에게 제공하는 방법입니다. CI/CD의 기본 개념은 지속적인 통합, 지속적인 서비스 제공, 지속적인 배포입니다. CI/CD는 새로운 코드 통합으로 인해 개발 및 운영팀에 발생하는 문제(일명 "인테그레이션 헬(integration hell)")을 해결하기 위한 솔루션입니다.

특히, CI/CD는 애플리케이션의 통합 및 테스트 단계에서부터 제공 및 배포에 이르는 애플리케이션의 라이프사이클 전체에 걸쳐 지속적인 자동화와 지속적인 모니터링을 제공합니다. 이러한 구축 사례를 일반적으로 "CI/CD 파이프라인"이라 부르며 개발 및 운영팀의 애자일 방식 협력을 통해 지원됩니다.
<img src="/assets/images/Git/CICD.png" />

## CI/CD 종류

- Jenkins
- CircleCI
- TravisCI
- Github Actions
- 그 외

# Github Action 개념

<img src="/assets/images/Git/github-workflow.png" />

## Workflows

Workflow는 직역하면 일의 흐름, 즉 **여러 Job으로 구성**되고 Event 실행(Trigger)가 자동화된 과정을 말한다. `.yaml(yml)`이라느 확장명으로 저장하며 `.github/workflows` 폴더에 저장된다.

[About workflows](https://docs.github.com/en/actions/using-workflows/about-workflows)

## Events

Workflow를 실행(Trigger)시키는 특정한 행동. 예를 들어 PullRequest를 생성하거나 commit된 내역을 push 하는 등을 말한다. 이미 Git을 사용해본적이 있다면 이미 Event를 해본적이 있을 것이다.

[Events that trigger workflows](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)

```
on:push
```

## Jobs

Job은 여러 Step(단계)루 구성되어 있고, 독립적으로도 실행가능하고, 다른 Job에 의존관계를 들 수도 있다. 기본적으로 workflow는 여러 개의 Job들을 병렬로 실행한다.

## Step

Task들의 집합으로, Job 안에서 어떤 명령어(예 : npm install 등)를 입력할 수 있고, 환경변수(`env`)도 설정할 수 있다

## Actions

Workflow의 가장 작은 블럭으로서, Job을 만들기 위해 Step들을 연결할 수도 있다. 일종의 라이브러리와 비슷한 개념으로, 재사용이 가능하며 [Github Marketplace](https://github.com/marketplace?type=actions)와 [Github Actions Repository](https://github.com/actions/)에서 확인 가능하다.

## Runners

Runner는 [Github Actions runner application](https://github.com/actions/runner)가 설치된 서버이다. GitHub Actions runner application는 GitHub Actions workflow으로부터 job을 실행시켜주는 어플리케이션이다. Runner는 한 번에 하나의 job을 실행시키며 과정, 로그, 결과를 기록해서 GitHub에게 돌려준다.

## 예시

```
.github/workflows/github-actions-example.yml
name: learn-github-actions
on: [push]
jobs:
  check-bats-version:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '14'
      - run: npm install -g bats
      - run: bats -v
```

#### 참고 영상

- [제발 깃허브 액션🔥 모르는 개발자 없게해 주세요 🙏](https://youtu.be/iLqGzEkusIw){% include video id="iLqGzEkusIw" provider="youtube" %}
- [GitHub Actions - Supercharge your GitHub Flow](https://youtu.be/cP0I9w2coGU){% include video id="cP0I9w2coGU" provider="youtube" %}
- [github.com - action](https://youtu.be/uBOdEEzjxzE){% include video id="uBOdEEzjxzE" provider="youtube" %}

#### 참조 문서 및 사이트

- [[GitHub Action Learning] #1 GitHub Actions 소개](https://callmemaru.com/posts/github-actions-learning-1/)
- [Github Action 사용법 정리](https://zzsza.github.io/development/2020/06/06/github-action/)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
