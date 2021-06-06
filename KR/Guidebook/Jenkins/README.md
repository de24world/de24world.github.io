[CI/CD] Jenkins
======================
# 1. CI (Continuous Integration) 
* 여러 개발자들의 코드를 계속해서 **통합**하는 것.

<img src="/KR/Guidebook/Jenkins/CI_Image.jpg" alt="CI_Image" title="CI-Image"></img>

# 2. CD (Continuous Delivery) 
* 개발자들이 코드를 계속 작성하면, 사용자 및 내부 사용자들 (즉, QA 등등)이 계속 쓸 수 있게 만드는 것. 즉, **지속적으로 배포가능한 상태를 유지**하는 것

# 3. Jenkins 란
<img src="/KR/Guidebook/Jenkins/jenkins_pipeline2.png" alt="jenkins_pipeline2" title="jenkins_pipeline2"></img>

* CI Tools (무료 오픈소스, 설치형) / 빌드, 테스트, 정적 분석을 자동으로 실행 해줌

* 젠킨스 이전? : build, test 명령어를 수동으로 터미널에서 입력
<img src="/KR/Guidebook/Jenkins/before_jenkins.png" alt="before_jenkins" title="before_jenkins"></img>

* 젠킨스 이후? : 일일이 build, test 명령어를 입력하지 않아도 코드만 commit 해서 push 하면 자동적으로 실행
<img src="/KR/Guidebook/Jenkins/after_jenkins.png" alt="after_jenkins" title="after_jenkins"></img>

아키텍처
<img src="/KR/Guidebook/Jenkins/architecture.png" alt="architecture" title="architecture"></img>


<img src="/KR/Guidebook/Jenkins/jenkins_pipeline.png" alt="jenkins_pipeline" title="jenkins_pipeline"></img>

****
# 4. 그 외
## 4.1 Travis CI, Circle CI, Team City 같은 클라우드형 서비스도 있다. (유료형)
## 4.2 Github, Bitbucket, Gitlab 등에서 자체적으로 제공도 한다. 예 : Github Action, Gitlab : CI/CD, Bitbucket : Pipelines (일부 서비스 유료)
## 4.3 정적 사이트를 Github를 통해 올리면 바로 자기네 서버에 배포해주는 Netlify나 Vercel 처럼 그 자체가 배포 자동화인 서비스도 있다.
***** 

## ○ 참고 영상
* [CI/CD가 뭔가요? (Feat. 젠킨스, Travis CI, Github Actions)](https://youtu.be/UbI0Q_9epDM)
* [빌드(Build)를 위한 Jenkins 설치 및 설정하기](https://youtu.be/m0tky1jyP-0)


## ○ 참조 문서 및 사이트
* [CI/CD가 뭔가요? | 얄코](https://www.yalco.kr/43_ci_cd/) 
* [CICD-Jenkins-정리](https://velog.io/@jellyb3ar/CICD-Jenkins-%EC%A0%95%EB%A6%AC)


