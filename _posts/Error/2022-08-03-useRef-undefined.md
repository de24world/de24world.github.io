---
layout: single
title: "useRef .current null Error"
categories: Error
tag:
  [
    useRef,
    useEffect,
    useState,
    useLayoutEffect,
    리액트,
    react,
    undefined,
    current,
    error,
    라이프사이클,
    LifeCycle,
  ]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# 에러

`useRef`를 사용시에 해당 ref(`observedRef`)를 console.log를 찍어보면 null로 찍힌다.

```tsx
function App() {
  const observedRef = useRef<HTMLInputElement>(null);
  console.log(observedRef.current);

  return (
    <div ref={observedRef} className="App">
      <h1>Hello CodeSandbox</h1>
      <h2>Start editing to see some magic happen!</h2>
    </div>
  );
}
```

# 해결방법

`useRef`는 리액트에서 DOM을 연결해주는 Hook으로써, 원하는 element에 ref 속성을 넣어주면 useRef가 객채를 반환하여 `current` 속성에 dom을 넣어준다. 바닐라 자바스크립트에서 `document.getElementbyId`. useRef 초기값에 어떤 값을 입력하더라도 `null`이 출력하게 되는데, 이는 리액트 라이프 사이클 특성상 렌더링이 완료되기 전에 useRef가 실행되기 때문이다. 이를 해결하기 위해서는 `useEffect(useLayoutEffect)`를 이용하자. 만약 useRef값(예:.current...)을 활용하고 싶다면 `useState`를 이용하여 상태를 만들자. 그렇지 않으면 해당 값은 `useEffect` 함수안에서만 사용 가능하기 때문이다.

```tsx
const [isObserver, setObserver] = useState<HTMLInputElement>(null);

useEffect(() => {
  setObserver(observedRef);
}, [observedRef]);

console.log(isObserver.current);
// isObserver로만 출력해도 된다.
```

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>useRef가 null이라고 나오는 이유는 리액트 Life Cycle 특성상 발생하는 문제이다 </li>
  <li>따라서 useRef 값을 확인해보고 싶으면 useEffect를 이용하여 렌더링 완료 후 사용하자 </li>
  <li>.current 값 등 useRef 값을 사용하고 싶으면 useState를 이용하여 상태를 만들자.</li>
</ul>
</div>

#### 참조 문서 및 사이트

- [useRef : Object is Possibly null 오류와 관련해서](https://velog.io/@otterp/useRef-Object-is-Possibly-null-%EC%98%A4%EB%A5%98%EC%99%80-%EA%B4%80%EB%A0%A8%ED%95%B4%EC%84%9C)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
