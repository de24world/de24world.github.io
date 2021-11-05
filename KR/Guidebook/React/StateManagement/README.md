# React State Management

## 목차

1. [시작하며(Getting Started)](#시작하며getting-started)
2. 기본기능(Basic Features)  
   a. [페이지들(Pages)](#페이지들pages)  
   b. Data Fetching

3. [Context-API](#context-api)  
   a. 장점
   b. 단점
   c. 이럴 때 사용하세요
4. [Redux](#Redux)
   a. 장점
   b. 단점
   c. 이럴 때 사용하세요
5. [Recoil](#Recoil)
6. [React-Query](#React-Query)
7. [Redux](#Redux)
8. [Mobx](#Mobx)
   form 과 같이 값을 관찰해야할 때 (observable)
9. [Recoil](#Recoil)
10. [React-Query](#React-Query)
11. [useSWR](#useSWR)

## 시작하며(Getting Started)

React는 `A → B` (B ← A 는 안된다) 라는 단방향의 디자인 패턴, `Flux`를 지향하고 있다. 따라서 이럴 때 생기는 문제, 증조할아버지(?) 컴포넌트에서 증손자(?) 컴포넌트까지 데이터를 `props`로 넘겨주려면 여러 단계 걸쳐서 줘야하는 `props drill`이라는 현상이 발생된다. 따라서 이를 해결하고자 여러가지 상태 관리 매니지먼트가 있다.

## Context-API (useReducer)

전역적(gloabal)인 데이터를 공유할 수 있도록 고안된 방법이다.

<img src="/React/StateManagement/context-api.png" alt="context-api" title="context-api"></img>

b. 장점

- 별도의 라이브러리가 필요 없다.
- 간단하다

c. 단점

- Provider 안에 포함된 모든 컴포넌트가 리렌더링이 되어 성능 최적화에 방해가 된다. (useMemo를 사용하거나 상태값/액션을 나눌 수 있지만 좋은 구조는 아니다)
- Context 추가할 때마다 Provider 로 매번 감싸줘야하기 때문에 Provider hell 을 야기할 수 있다.

d. 이럴 때 사용하세요

- low-freqeuncy, 즉 낮은 빈도로 상태값이 변경할 때.
- 로그인 정보 또는 웹사이트 내에 사용자 설정 파일, 테마, 언어, 모달(Modal), 알림창(Alert) 등 상태값이 자주 바뀌지 않는 경우, 컴포넌트 간 간단한 공유 데이터에 사용됩니다.
- 즉 Child Component가 많지 않을 때 사용하는 것을 추천한다

## Context-API

리액트 16.3 버전부터 전역적(gloabal)인 데이터를 공유할 수 있도록 `Context Api` 새로 고안되었다.

<img src="/React/StateManagement/context-api.png" alt="context-api" title="context-api"></img>

b. 장점

- 별도의 라이브러리가 필요 없다.
- 간단하다

c. 단점

- Provider 안에 포함된 모든 컴포넌트가 리렌더링이 되어 성능 최적화에 방해가 된다. (useMemo를 사용하거나 상태값/액션을 나눌 수 있지만 좋은 구조는 아니다)
- Context 추가할 때마다 Provider 로 매번 감싸줘야하기 때문에 Provider hell 을 야기할 수 있다.

d. 이럴 때 사용하세요

- low-freqeuncy, 즉 낮은 빈도로 상태값이 변경할 때.
- 로그인 정보 또는 웹사이트 내에 사용자 설정 파일, 테마, 언어, 모달(Modal), 알림창(Alert) 등 상태값이 자주 바뀌지 않는 경우, 컴포넌트 간 간단한 공유 데이터에 사용됩니다.
- 즉 Child Component가 많지 않을 때 사용하는 것을 추천한다

## Redux

전역적(gloabal)인 데이터를 공유할 수 있도록 고안된 방법이다.

<img src="/React/StateManagement/with-redux.png" alt="with-redux" title="with-redux"></img>

b. 장점

- 별도의 라이브러리가 필요 없다.
- 간단하다

c. 단점

- Provider 안에 포함된 모든 컴포넌트가 리렌더링이 되어 성능 최적화에 방해가 된다. (useMemo를 사용하거나 상태값/액션을 나눌 수 있지만 좋은 구조는 아니다)
- Context 추가할 때마다 Provider 로 매번 감싸줘야하기 때문에 Provider hell 을 야기할 수 있다.

d. 이럴 때 사용하세요

- low-freqeuncy, 즉 낮은 빈도로 상태값이 변경할 때.
- 로그인 정보 또는 웹사이트 내에 사용자 설정 파일, 테마, 언어, 모달(Modal), 알림창(Alert) 등 상태값이 자주 바뀌지 않는 경우, 컴포넌트 간 간단한 공유 데이터에 사용됩니다.
- 즉 Child Component가 많지 않을 때 사용하는 것을 추천한다

## ○ 참고 영상

- [왜 Recoil을 써야하는가?](https://youtu.be/H10KNVxF6_s)
- [ARIA에 대해서 HTML 접근성 향상시키기](https://youtu.be/MQHNTzdqet0)

## ○ 참조 문서 및 사이트

- [리액트 상태 관리 가이드](https://www.stevy.dev/react-state-management-guide)
- [리덕스 잘 쓰고 계시나요?](https://ridicorp.com/story/how-to-use-redux-in-ridi/)
- [웹 폰트 사용과 최적화의 최근 동향](https://d2.naver.com/helloworld/4969726)
