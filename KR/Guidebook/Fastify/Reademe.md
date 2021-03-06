[Fastify]] Fastify
======================
# 1. Fastify? 
* 최소한의 오버헤드와 강력한 플러그인 아키텍처로 최고의 개발 경험을 제공하는데에 초점을 맞춘 웹 프레임워크이며, 현재 가장 빠른 NoedJS기반 웹 프레임워크 중 하나이다.

## 1.1 핵심 기능 (Core features)
* 빠른 속도 : 모두 아시다시피 한 Fastify는 가장 빠른 웹 프레임워크 중에 하나이며, 코드의 복잡성에 따라 초당 최대 30,000 번의 요청 작업을 실행할 수 있습니다. 
* 확장성: Fastify는 hooks, plugins 그리고 decorators들 통하여 최대한 확장할 수 있습니다.
* Schema 기반 : [Json 스키마](https://json-schema.org/)를 사용하여 경로를 검증하고 출력을 직렬화하는 것이 필수 사항이 아니더라도 내부적으로 Fastify는 고성능 함수로 스키마를 컴파일합니다.
* Logging : 로그는 매우 중요하지만 비용이 보통 많이 든다. 이 비용을 제거하기 위해 최고의 로거를 사용합니다. [Pino](https://github.com/pinojs/pino/)
* 개발자 친화적 : 퍼포먼스와 보안 희생 없이 만들어진 개발적 친화적인 프레임워크이다.
* Typescript ready : 성장하고 있는 타입스크리트 커뮤니티를 지원할 수 있도록 Typescript 유형 선언 파일을 유지하기 위해 Fastify는 노력하고 있습니다.


# 2. Quick Start
* 필수로 알아야하는 지식 : Javascript, Node.js, NPM 등
* [공식 홈페이지 참조](https://www.fastify.io/)

## 2.1 NPM을 통한 설치

```
npm install fastify
```

## 2.2 `server.js` 를 먼저 생성한다.
```javascript
// 먼저 필요한 Framework, fastify 를 불러오고 인스턴스화 시키자
const fastify = require('fastify')({ logger: true })

// route 선언한다.
fastify.get('/', async (request, reply) => {
  return { hello: 'world' }
})

// 서버를 실행시킨다.
const start = async () => {
  try {
    await fastify.listen(3000)
  } catch (err) {
    fastify.log.error(err)
    process.exit(1)
  }
}
start()
```

## 2.3 아래의 명령어를 통하여 서버를 실행시켜준다.
```
node server
```

## 2.4 locahost:3000에서 테스트 할 수 있다.
```
curl http://localhost:3000
```


# 3. 요청/읍답 유효성 검사 및 Hooks (Request/Response validation and hooks) 
* 물론, Fastify 로 더 많은 것을 할 수 있습니다.
예를 들면, JSON 스키마(Schema) 를 사용하여 입력 및 출력 유효성 검사를 쉽게 재공하고 핸드러가 실행되기 전에 특정 작업을 수행할 수 있습니다.

```javscript
const fastify = require('fastify')({ logger: true })

fastify.route({
  method: 'GET',
  url: '/',
  schema: {
    // 요청(request)들은 'name'이라는 매개변수가 있는 쿼리 문자열이 있어야 합니다.
    querystring: {
      name: { type: 'string' }
    },
    // 응답(request)은 '문자열' 유형의 'hello' 속성 객체여야 합니다.
    response: {
      200: {
        type: 'object',
        properties: {
          hello: { type: 'string' }
        }
      }
    }
  },
  // 이 함수는 핸들러가 실행되기 전에 모든 요청에 대해 실행됩니다.
  preHandler: async (request, reply) => {
    // 예를 들어 인증 확인을 할 수 있습니다.
  },
  handler: async (request, reply) => {
    return { hello: 'world' }
  }
})

const start = async () => {
  try {
    await fastify.listen(3000)
  } catch (err) {
    fastify.log.error(err)
    process.exit(1)
  }
}
start()

```



## 1.4 가격
* [홈페이지 참조](https://lokalise.com/pricing)

***

# 2. 사용방법 

## 2.1 Github 연결방법
* [How to sync Github & Lokalise | Enterprise localization expert](https://youtu.be/AKaE_2Q4yBY)

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
        주말을 4제000외한 주중에 9시부터 16시 사이에 2시간에 한번씩 빌드를 수행
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
* [Fastify Crash Course | Node.js Framework](https://youtu.be/Lk-uVEVGxOA)
* [빌드(Build)를 위한 Jenkins 설치 및 설정하기](https://youtu.be/m0tky1jyP-0)


## ○ 참조 문서 및 사이트
* [Swagger란]](https://benjaminwoojang.medium.com/fastify-%EA%B8%B0%EC%B4%88-%ED%95%99%EC%8A%B5%ED%95%98%EA%B8%B0-c6e1dbf7c978) 
* [CICD-Jenkins-정리](https://velog.io/@jellyb3ar/CICD-Jenkins-%EC%A0%95%EB%A6%AC)
* [3.3.3 Build Triggers (빌드 유발)](https://blog.naver.com/special9486/220274932377)

