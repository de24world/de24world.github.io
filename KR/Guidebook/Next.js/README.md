# Next.js 공홈 번역본

* Updated date 2021.07.19
* next.js 공식 홈페이지 번역본입니다. (https://nextjs.org/docs/)
까지 반영되어 있습니다.

## 목차
  1. [시작하며(Getting Started)](#시작하며getteing-started)
  2. [기본기능(Basic Features)](#변수variables)   
    a. Pages   
    b. Data Fetching
  3. [라우팅(Routing)](#함수functions)
  4. [API Routes(API routes)](#함수functions)
  5. [프로덕션으로 이동(Going to Production)]



## 시작하며(Getting Started)
Next.js 문서에 오신 것을 환영합니다.
만약 새로운 Next.js가 처음이시라면 해당 [수업](https://nextjs.org/learn/basics/create-nextjs-app)을 먼저 시작하는 것을 추천드립니다.
퀴즈와 함께 다양한 수업들을 통해 당신이 어떻게 Next.js를 사용하는지 알 수 있게 될 것입니다.
Next.js 와 관련된 어떠한 질문이 있다면, Next.js의 커뮤니티에 [Github Discussions](https://github.com/vercel/next.js/discussions) 물어보는 것을 언제든 환영합니다.

#### 시스템 요구사항 (System Reuqirements)
- [Node.js 12](https://nodejs.org/en/) 혹은 그 이상 
- MacOS, Windows(WSL 포함), 그리고 Linux 역시 지원합니다.

### 설치(Setup)
우리는 `create-next-app`과 함께 Next.js 앱을 새로 생성하는 것을 추천드리며, 모든 것을 자동적으로 세팅해드립니다. 프로젝트 생성시 아래와 같이 입력해줍니다:

```
npx create-next-app
# 혹은
yarn create next-app
```

만약 타입스크립트로 시작하시는 것을 원하시면 `--typescript` 명령어를 함께 입력해줍니다.

```
npx create-next-app --typescript
# 혹은
yarn create next-app --typescript
```

설치가 완료되었다면, development 서버를 시작해줍니다. `pages/index.js` 해당 파일에서 수정하고, 브라우저에서 결과를 확인하실 수 있습니다.
`create-next-app`을 어떻게 사용하는지 자세히 알고 싶다면, [`create-next-app` 문서](https://nextjs.org/docs/api-reference/create-next-app)에서 리뷰하실 수 있습니다.



  4. [객체와 자료구조(Objects and Data Structures)](#객체와-자료구조objects-and-data-structures)
## **객체와 자료구조(Objects and Data Structures)**