[CI/CD] Jenkins
======================
# 1. CI (Continuous Integration) 
* 여러 개발자들의 코드를 계속해서 **통합**하는 것.

<img src="/KR/Guidebook/Jenkins/CI_Image.jpg" alt="CI_Image" title="CI-Image"></img>

# 2. CD (Continuous Delivery) 
* 개발자들이 코드를 계속 작성하면, 사용자 및 내부 사용자들 (즉, QA 등등)이 계속 쓸 수 있게 만드는 것. 즉, **지속적으로 배포가능한 상태를 유지**하는 것

# 3. Jenkins 란
* CI Tools (무료 오픈소스, 설치형) / 빌드, 테스트, 정적 분석을 자동으로 실행 해줌
<img src="/KR/Guidebook/Jenkins/jenkins_pipeline2.png" alt="jenkins_pipeline2" title="jenkins_pipeline2"></img>


* 젠킨스 이전? : build, test 명령어를 수동으로 터미널에서 입력
<img src="/KR/Guidebook/Jenkins/before_jenkins.png" width="450px" alt="before_jenkins" title="before_jenkins"></img>

* 젠킨스 이후? : 일일이 build, test 명령어를 입력하지 않아도 코드만 commit 해서 push 하면 자동적으로 실행
<img src="/KR/Guidebook/Jenkins/after_jenkins.png" width="450px" alt="after_jenkins" title="after_jenkins"></img>

아키텍처
<img src="/KR/Guidebook/Jenkins/architecture.png" width="450px" alt="architecture" title="architecture"></img>

***
## 3.1 Jenkins 설치
* [Jenkins 공식 홈페이지 다운로드 링크](https://www.jenkins.io/download/)   
* 공식 홈페이지에서 사용자 환경에 맞게 다운로드하여 설치   
* 설치 방법은 아래의 참조 영상 [빌드(Build)를 위한 Jenkins 설치 및 설정하기](https://youtu.be/m0tky1jyP-0) 참조


## 3.2 Jenkins Plugin
* 젠킨스의 장점 중 하나는 다양한 플러그인으로 기능을 확장 할 수 있다.   
*  예를 들어 git plugin을 설치하면 git과 jenkins를 쉽게 연동할 수 있다.


## 3.3 Jenkins 설정
* Jenkins 접속하여 새로 생성하고 싶으면 왼쪽 메뉴에 **New Item** 을 클릭하여 Freestyle project(혹은 다르게도 가능)을 눌러 새 작업을 생성해준다.
<img src="/KR/Guidebook/Jenkins/jenkins_configure.png" alt="jenkins_configure" title="jenkins_configure"></img>


 ### 3.3.1 General
프로젝트에 대한 설명, url, discard old builds(오래된 빌드 삭제) 등 전반적인 설정을 한다.

 ### 3.3.2 Source Code Management (소스 코드 관리)
 Repositories 설정 (URL, 인증)을 할 수 있으며, 어떤 Branches 들을 build 할 것인지 설정할 수 있다.   
public 레포지토리는 credentials(인증) 설정할 필요가 없으나, private 레포지토리는 git 과 연동하여 설정해야한다.

 ###  3.3.3 Build Triggers (빌드 유발)
빌드를 언제 실행할 지를 설정할 수 있다.   
    **Trigger builds remotely (e.g., from scripts) 빌드를 원격으로 유발** : 외부에서 URL을 통해 빌드를 진행 할 수 있도록 설정합니다.   
    **Build after other project are built** : 다른 프로젝트를 빌드한 후 이어서 현재 프로젝트를 빌드하는 설정.    
    **Build periodically** : 주기적으로 빌드   
    **Poll SCM** : 서버에서 변경된 사항이 존재할 때 빌드를 수행하는 설정     

        ```
        schedule 예시
        15분 간격으로 빌드 작업을 수행
        H/15 * * * *
        모든 시간의 첫 30분 동안에 10분 간격으로 빌드를 수행
        H(0-29)/10 * * * *
        주말을 제외한 주중에 9시부터 16시 사이에 2시간에 한번씩 빌드를 수행
        H 9-16/2 * * 1-5
        12월 달은 제외하고 매달 1일과 15일에 한번씩 빌드를 수행
        H H 1,15 1-11 * 
        ```


 ### 3.3.4 Build Environment

 ### 3.3.5 Build 

### 3.3.6 Post-build Actions 


****
# 4. 그 외
* Travis CI, Circle CI, Team City 같은 클라우드형 서비스도 있다. (유료형)
* Github, Bitbucket, Gitlab 등에서 자체적으로 제공도 한다. 예 : Github Action, Gitlab : CI/CD, Bitbucket : Pipelines (일부 서비스 유료)
* 정적 사이트를 Github를 통해 올리면 바로 자기네 서버에 배포해주는 Netlify나 Vercel 처럼 그 자체가 배포 자동화인 서비스도 있다.
***** 

## ○ 참고 영상
* [CI/CD가 뭔가요? (Feat. 젠킨스, Travis CI, Github Actions)](https://youtu.be/UbI0Q_9epDM)
* [빌드(Build)를 위한 Jenkins 설치 및 설정하기](https://youtu.be/m0tky1jyP-0)


## ○ 참조 문서 및 사이트
* [CI/CD가 뭔가요? | 얄코](https://www.yalco.kr/43_ci_cd/) 
* [CICD-Jenkins-정리](https://velog.io/@jellyb3ar/CICD-Jenkins-%EC%A0%95%EB%A6%AC)
* [3.3.3 Build Triggers (빌드 유발)](https://blog.naver.com/special9486/220274932377)

