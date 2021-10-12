[다이나믹 일드(Dynamic Yield)] 
======================
# 1. Dynamic Yield는?
* Dynamic Yield 는 `개인화 마케팅 툴`이다. 개인화 마케팅이란 소비자 개개인의 사이트 내에서의 행동, 지난 구매 이력, 프로필 등 데이터를 조합하여, 해당 고객에게 최적화된 경험을 제공함을 통해 가치를 창출하는 마케팅 활동이다. 다이나믹 일드의 주요 기능의 다음과 같다.

# 1. 1 고객 데이터 관리/분석(Customer Data Management/ Analysis)
* 다이나믹 일드는 고객의 정량적인 데이터 뿐만 아니라 고객이 사이트 내에서 움직이는 행동 패턴을 파악하여 고객의 제품/ 서비스에 대한 선호도나 관심 분야를 파악하는 contextual 분석을 통해 고객 데이터를 수집한다.

예를들어 어떤 고객이 사이트에 들어와서, 파란색 여성 자켓을 클릭하고 장바구니에 담고, 다시 여성 세일 카테고리를 훑어본다고 하자. 이때 다이나믹 일드가 이 고객의 관심사(Affinity) 정보를 아래와 같이 수집한다.
<img src="/KR/Guidebook/DynamicYield/dy_affinity.png" alt="dy_affinity" title="dy_affinity"></img>

이후 이 고객의 사이트 화면에는, 고객이 좋아할만한 ‘여성 의류’, 특히 고객이 좋아한다고 수집된 ‘파란색’류의 제품을 추천하게 된다.

이러한 개인 관심도 모델링 (Individual Affinity Modeling)이 다이나믹 일드가 다른 개인화 툴에 비해 특장점으로 가지고 있는 기능이다.

다이나믹 일드의 또다른 장점은 동일한 고객이 여러 디바이스나 다양한 채널들을 통해 접속해도 CUID(Customer Unique Identifier)를 통해 해당 고객의 데이터를 일관성있게 유지한다는 점이다.

이렇게 수집된 정보는 회사의 포스(POS) 시스템이나, 다른 시스템에도 연동하여 사용할 수 있다. 반대로 포스 데이터를 다이내믹 일드에 연동할 수도 있다.

수집된 고객 정보는 다이나믹 일드 어드민 사이트의 ‘Audience Explorer’ 메뉴에서 아래와 같이 보기 쉽게 정리된다. 이곳에서 간단하게 고객의 프로필이나 발생한 이벤트 등을 조합하여, 고객 세그먼트를 생성하여 고객 그룹을 관리할 수도 있다.

<img src="/KR/Guidebook/DynamicYield/audience_explorer.png" alt="dy_audience_explorer" title="dy_audience_explorery"></img>




# 2. WAI-ARIA
* WAI-ARIA는 웹 페이지, 특히 동적 콘텐츠, 그리고 Ajax, HTML, 자바스크립트 및 관련 기술로 개발된 사용자 인터페이스 구성 요소의 접근성을 증가시키는 방법에 대해 규정한 W3C가 출판한 기술 사양이다

## 2.1 role (역할)
    
```jsx
    <a href="" role="button">팝업</a>
```

## 2.2 property (속성)
    
```html
   <label for="id">아이디</label>
   <input type="text" id="id" aria-required="true">
```

## 2.3 state (상태)
    
```html
   <button aria-expanded="true">열기</button>
   <div hidden>열기 내용</div>
```


# 3. Jenkins 란
* CI Tools (무료 오픈소스, 설치형) / 빌드, 테스트, 정적 분석을 자동으로 실행 해줌
<img src="/KR/Guidebook/Jenkins/jenkins_pipeline2.png" alt="jenkins_pipeline2" title="jenkins_pipeline2"></img>


* 젠킨스 이전? : build, test 명령어를 수동으로 터미널에서 입력   
<img src="/KR/Guidebook/Jenkins/before_jenkins.png" width="450px" alt="before_jenkins" title="before_jenkins"></img>

* 젠킨스 이후? : 일일이 build, test 명령어를 입력하지 않아도 코드만 commit 해서 push 하면 자동적으로 실행   
<img src="/KR/Guidebook/Jenkins/after_jenkins.png" width="450px" alt="after_jenkins" title="after_jenkins"></img>

* 아키텍처   
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
    - Trigger builds remotely (e.g., from scripts) 빌드를 원격으로 유발 : 외부에서 URL을 통해 빌드를 진행 할 수 있도록 설정합니다.   
    - Build after other project are built : 다른 프로젝트를 빌드한 후 이어서 현재 프로젝트를 빌드하는 설정.    
    - Build periodically** : 주기적으로 빌드   
    - Poll SCM** : 서버에서 변경된 사항이 존재할 때 빌드를 수행하는 설정     

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

### 3.3.6 Post-build Actions 
빌드 이후 액션을 설정해줄 수 있다. (예, 이메일 알림 등)

****
# 4. 그 외
* Travis CI, Circle CI, Team City 같은 클라우드형 서비스도 있다. (유료형)
* Github, Bitbucket, Gitlab 등에서 자체적으로 제공도 한다. 예 : Github Action, Gitlab : CI/CD, Bitbucket : Pipelines (일부 서비스 유료)
* 정적 사이트를 Github를 통해 올리면 바로 자기네 서버에 배포해주는 Netlify나 Vercel 처럼 그 자체가 배포 자동화인 서비스도 있다.
***** 

## ○ 참고 영상
* [웹접근성 향상을 위한 방법](https://youtu.be/g8-Y8dHQ22Y)ㄴ


## ○ 참조 문서 및 사이트
* [고객 경험 개인화 온사이트 마케팅 툴 -다이나믹 일드 (Dynamic yield)](https://cassey.kr/dynamic_yield)
* [클린코드란 무엇인가?](https://www.samsungsds.com/kr/story/cleancode-0823.html)
