[웹접근성과 웹표준(Web Accessibility & Web Standards)] 
======================
# 1. 웹표준 (Web Standards) 이란?
* 웹표준은 어떠한 운영체제나 브라우저를 사용하여도 동일한 콘텐츠를 볼 수 있도록 웹에서 표준적으로 사용되는 기술이나 규칙을 말한다.
    - W3C에서 웹 표준이 확정되는 순서   
    <img src="/KR/Guidebook/웹접근성/process.png" alt="how_decide_web_standard" title="how_decide_web_standard"></img>

## 1.1 웹 표준이 가져다주는 장점
* 검색엔진 최적화
* 개발자가 더 이해하기 쉬운 코드
* 구조와 표현의 분리

# 2. 웹접근성 (Web Accessibility) 이란?
* 개인의 능력에 상관없이 모든 사람엑 웹을 사용할 수 잇또록 하는 방법
    - 장애인 및 고령자를 포함한 모든 사람 (예: 스크린 리더를 통한 시각 장애인이 웹을 사용할 수 있도록 해준다.)

# 3.WAI-ARIA
* WAI-ARIA는 웹 페이지, 특히 동적 콘텐츠, 그리고 Ajax, HTML, 자바스크립트 및 관련 기술로 개발된 사용자 인터페이스 구성 요소의 접근성을 증가시키는 방법에 대해 규정한 W3C가 출판한 기술 사양이다

## 3.1 role (역할)
    
```html
    <a href="" role="button">팝업</a>
```

## 3.2 property (속성)
    
```html
   <label for="id">아이디</label>
   <input type="text" id="id" aria-required="true">
```

## 3.3 state (상태)
    
```html
   <button aria-expanded="true">열기</button>
   <div hidden>열기 내용</div>
```


#
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
* [ARIA에 대해서 HTML 접근성 향상시키기](https://youtu.be/MQHNTzdqet0)


## ○ 참조 문서 및 사이트
* [국가별 웹접근성 정책](https://www.w3.org/WAI/policies)
* [aria-label 속성 사용](https://developer.mozilla.org/ko/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-label_attribute) 
* [웹접근성](https://www.w3.org/TR/wai-aria/#aria-label)
* [웹 접근성 어디까지 신경써봤니?](https://velog.io/@dev-tinkerbell/%EC%9B%B9%EC%A0%91%EA%B7%BC%EC%84%B1-%EC%96%B4%EB%94%94%EA%B9%8C%EC%A7%80-%EC%8B%A0%EA%B2%BD%EC%8D%A8%EB%B4%A4%EB%8B%88)

