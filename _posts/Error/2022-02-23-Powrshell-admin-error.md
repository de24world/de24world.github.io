---
layout: single
title: "cannot be loaded because running scripts is disabled on this system"
categories: Error
tag: [Error, fwlink, microsoft, yarn, npm]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}


만약 보안문제로 윈도우 계정 로그인해야하는 회사(공용) 컴퓨터 혹은 노트북의 경우 Visual Studio Code의 Terminal에서 `npm`이나 `yarn` 패키지 설치 혹은 실행하려고 하면 아래의 에러 메세지가 뜬다.

```
yarn : File C:\Users\...\AppData\Roaming\npm\yarn.ps1 cannot be loaded because running scripts is disabled on this system. For more information, see about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170.

```

이럴 경우 아래의 과정데로 실행해보자.

1.  window PowerShell 프로그램을 관리자 권한으로 실행한다.
<img src="/assets/images/Error/window-powershell.png"/>

2. `Get-ExecutionPolicy` 명령어를 실행해본다. 만약 `RemoteSigned`이 아니라 `Restricted`로 되어 있다면 권한을 변경하자.

3. `Set-ExecutionPolicy RemoteSigned` 입력하고 다시 `Get-ExecutionPolicy` 입력해서 `RemoteSigned`로 변경되었는지 확인해본다.

4. 변경되었다면 이제 Terminal에서 package 명령어 실행될 것이다.

#### 참조 문서 및 사이트

- [[PowerShell] 이 시스템에서 스크립트를 실행할 수 없으므로 파일을 로드할 수 없습니다. 자세한 내용은about_Execution_Policies(https://go.microsoft.com/fwlink/?LinkID=135170)를 참조하십시오](https://dog-developers.tistory.com/183)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
