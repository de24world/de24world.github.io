[cloudflare ] 클라우드 플레어
======================
# 1. cloudflare ? 
* Cloudflare는 인터넷에 연결하는 모든 것을 안전하고 비밀을 유지하면서 신속하고 안정적으로 연결하도록 설계된 전역 네트워크입니다.
    - 웹 사이트, API, 인터넷 응용프로그램을 보안합니다.
    - 기업 네트워크, 직원, 장치를 보호합니다.
    - 네트워크 에지에서 실행되는 코드를 작성하고 배포할 수 있습니다

## 1.1 Lokalise 장점
* 단일 작업 공간에서 팀원들과 협업(콜라보)할 수 있습니다. 예를 들어, 업무(Tasks)를 할당(assign)하고 진행사항(progress)을 추적(track)하고, 누가 언제 무엇을 했는지 Lokalise 내에서 확인할 수 있습니다.
* 개발 주기에 병행하여(맞춰) 현지화 작업을 진행할 수 있습니다. 예를 들어, Adobe XD, Figma 및 Sketch 디자인 툴들과 작업을 함께 할 수 있으며, 그 작업이 끝날 때까지 기다릴 필요가 없습니다. 
* Lokalise 제품 내에 내장된 도구를 사용하세요. 번역 메모리, 자동 번역 그리고 QA를 체크할 수 있습니다. 제품의 스크린샷을 이용하여 해당 스크린샷을 텍스트를 번역할 수도 있습니다.
* 현지화 작업의 번거로움을 덜어낼 수 있습니다. Mobile SDKs, API, CLI 등의 시간을 절약할 수 있으며, Github, Bitbucket, Gitlab, Azure의 레포(Repos)들 혹은 Jira와 통합하여 개발자의 작업을 줄일 수 있습니다.

## 1.2 Lokalise 어디에 사용 가능한가?
* 웹 앱 : frontend, bakcend, single page, blogs 등 어떤 웹 앱에 사용 가능합니다.
* 모바일 앱 :  어떠한 모바일 Platform 언어 파일에도 업로드 가능합니다. 원한다면 Embed Lokalise IOS SDK 혹은 Lokalise Android SDK 가능합니다.
* 게임 : 당사의 클라우드 소포트웨어드는 전 세계의 많은 주요 게임 개발자로부터 신뢰를 받고 있습니다.
* 문서 : 당신의 DOCX 혹은 정적인 HTML 파일을 업로드하세요.
* 마케팅 자산 : 웹 페이지, 블로그, 이메일 및 기타 마케팅 자산을 고객이 사용하는 언어로 말하게 하여, 참여도 및 전화율을 높이세요. HubSport, Contentful 및 Storyblok과 Lokalise 통합하여 현지화 작업을 신속하게 제어할 수 있습니다.
* IoT : 가장 많이 사용되는 현지화 파일 형식을 지원합니다.

# 2. 클라우드 서비스 모델이란
* 클라우드 컴퓨팅은 다음 컴퓨팅 모델 중 하나에 속합니다. 클라우드 서비스 모델은 3가지로 나뉘어지며, 이러한 모델은 클라우드 공급자와 클라우드 사용자가 서로 다른 수준을
 관리하게 됩니다.
***
## 2.1 laas(Infrastructure as a service)
* 우리가 자주 사용하는 가상 호스팅(VM Hosting)과 비슷하나 처음에 말했다시피, 가상 호스팅은 우리가 직접 장비를 사서 그 장비의 한에서 자원을 할당하고 구성해야 하지만, IaaS는 기업이 준비해놓은 환경에서 우리가 선택할 수 있다는 점에서 차이가 있습니다.
* 일반적으로 적은 OS가 지원됩니다. (아마존은 일부 Linux와 Windows Server 제공)
* 고객은 OS와 어플리케이션을 직접 관리해야 합니다.
* 관리 측면에서 개발자와 인프라 관리자의 역할을 분담시킬 수 있습니다.

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
    - Trigger builds remotely (e.g., from scripts) 빌드를 원격으로 유발 : 외부에서 URL을 통해 빌드를 진행 할 수 있도록 설정합니다.   
    - Build after other project are built : 다른 프로젝트를 빌드한 후 이어서 현재 프로젝트를 빌드하는 설정.    
    - Build periodically** : 주기적으로 빌드   
    - Poll SCM** : 서버에서 변경된 사항이 존재할 때 빌드를 수행하는 설정  (플러그인)   

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


 ### 3.3.4 Build Environment (빌드 환경)
 빌드 환경 설정
    - Delete workspace before build start : 빌드를 실행하기 전, 이전에 사용되던 작업 공간 삭제 
    - Use secret text(s) or file(s) : 다양한 자격 증명에 사용할 인증 파일 또는 텍스트 사용    
    - Abort the build if it’s struck : 빌드가 교착 상태 등의 이유로 중지되면 지정된 시간 내로 빌드 종료 후 지정된 메시지 출력    
    - Add timestamps to the Console Output : 빌드 시작 시간, 빌드 종료 시간 등 시간과 관련된 내용을 Console output에 함께 출력  
    - With Ant : Apache Ant를 사용하여 빌드하는 환경 구성. 

 ### 3.3.5 Build (빌드)
 명령어 입력 등 다양한 방법으로 빌드 시킬 수 있다.   
    - Execute Windows batch command: 입력된 Window command line 실행   
    - Execute Shell: sh -xe 명령어 실행. Linux 전용.   
    - Invoke Ant: Ant 빌드 시스템을 사용하는 프로젝트의 경우에 사용. 입력된 인자를 통해 빌드   
    - Invoke Gradle script: Gradle를 빌드 시스템으로 빌드하는 프로젝트의 경우에 사용. 입력된 인자를 통해 작업.   
    - Invoke top-level Maven targets: Maven 빌드 시스템으로 빌드하는 프로젝트의 경우에 사용. 입력된 인자를 통해 작업   
    - Run with timeout: 지정된 시간동안 빌드가 완료되지 않으면 빌드 중지   
    - Set build status to “pending” on GitHub commit: Git 프로젝트 속성에 정의된 이름 속성으로 작업 이름을 대체    

### 3.3.6 Post-build Actions (빌드 후 조치)
빌드 이후 액션을 설정해줄 수 있다. (예, 이메일 알림 혹은 Projects to build : 다른 프로젝트와 파이프라인 설정 등을 할 수 있다.)


# 4. Pipeline (파이프라인)
* 파이프라인이란 Jenkins Job(작업), 즉 빌드/테스트/배포 등을 Job(작업)이라고 부르는데 이를 연속적으로 수행 가능하도록 만들 수 있는 기능을 말한다.
* 새로운 아이템(New Item)을 클릭하여 새로운 작업을 만들 때, Pipeline을 설정해주면 된다.   

<img src="/KR/Guidebook/Jenkins/jenkins_pipeline_script.png" alt="jenkins_pipeline_script" title="jenkins_pipeline_script"></img>   
    - Pipeline script : 스크립트로만 파이프라인을 정의한다.   
    - Pipeline script from SCM : 서버에서 변동사항이 있을 때 스크립트 실행(위의 Poll SCM 참조)

****
# 5. 그 외
* Travis CI, Circle CI, Team City 같은 클라우드형 서비스도 있다. (유료형)
* Github, Bitbucket, Gitlab 등에서 자체적으로 제공도 한다. 예 : Github Action, Gitlab : CI/CD, Bitbucket : Pipelines (일부 서비스 유료)
* 정적 사이트를 Github를 통해 올리면 바로 자기네 서버에 배포해주는 Netlify나 Vercel 처럼 그 자체가 배포 자동화인 서비스도 있다.
***** 

## ○ 참고 영상
* [Cloudflare Introduction (Tutorial for Beginners)](https://youtu.be/7riFvux9Bw4)
* [빌드(Build)를 위한 Jenkins 설치 및 설정하기](https://youtu.be/m0tky1jyP-0)


## ○ 참조 문서 및 사이트
* [클라우드 컴퓨팅, IaaS, PaaS, SaaS이란?](https://wnsgml972.github.io/network/2018/08/14/network_cloud-computing/) 
* [CICD-Jenkins-정리](https://velog.io/@jellyb3ar/CICD-Jenkins-%EC%A0%95%EB%A6%AC)
* [3.3.3 Build Triggers (빌드 유발)](https://blog.naver.com/special9486/220274932377)

