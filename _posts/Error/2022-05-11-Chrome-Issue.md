---
layout: single
title: "Chrome Error, 크롬 에러"
categories: Error
tag: [크롬, Chrome, scrollIntoView]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

<img src="/assets/images/CLS/width_height.gif" />

# 크롬(Chrome)

### scrollIntoView({ behavior: 'smooth', ... })

스크롤 이벤트가 크롬에서 2-3번 정도 작동 안하다가 이동하고자 하는 부분 조금 보이고 난 뒤에는 정상 작동하는 경우가 발생하였다.(정확히는 원하고자하는 부분 위에 이동 되었다) 유독 이상하게 크롬에서만 발생하고 파이어폭스에서는 바로 첫번째에 원하는 화면에 스크롤이 클릭뒤에 이동되었다. 검색결과 `scrollIntoView({ behavior: 'smooth', ... })` 함수 내에서 `behavior: 'smooth'` 부분이 문제였다. 검색 결과 크롬 최신버전이 scroll smooth 관련하여 문제가 있는거 같아, `behavoir: 'smooth'`를 삭제하니 스크롤 기능 잘 작동하였다(단, smooth하게 되지는 않는다)

혹은 `chrome://flags/#smooth-scrolling` 옵션으로 들어가서 `Smooth Scrolling` 설정이 키면 된다고 하나 대부분 사용자들은 default이기 때문에 그냥 smooth를 제거해주었다.

[stackoverflow 참조](https://stackoverflow.com/questions/61885401/scrollintoview-is-not-working-in-chrome-version-81-behaviour-smooth-is-not-hap)
