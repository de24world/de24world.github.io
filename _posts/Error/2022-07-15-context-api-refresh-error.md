---
layout: single
title: "refresh(새로고침)시 Context API State undefined 에러"
categories: Error
tag:
  [
    Next.js,
    넥스트,
    리액트,
    router,
    라우터,
    useRouter,
    Context Api,
    useContext,
    Provider,
    state,
    에러,
    error,
    rerender,
    refresh,
    리렌더링,
    localStorage,
    SessionStorage,
    새로고침,
  ]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# 에러

Context API를 이용하여 state를 전역관리하고 있다. 그런데 `router.push`를 이용하면 state 업데이트가 공유가 되지 않고 있다. 혹은 새로 고침시에도 state가 찾을 수 없다고 한다.

# 해결방법

이럴 때는 `localStorage`을 활용해보자. 리액트 사용자는 localStorage를 custom Hook, utils, Context API와 결합하여 사용할 수도 있다. (중요한 정보의 경우 `SessionStorage`를 이용하자)

\*localStorage : 데이터를 사용자 로컬에 보존하는 방식으로, 데이터를 저장하고 덮어쓰기, 삭제 등 자바스크립트로 조작이 가능하며, 모바일에서 사용이 가능하다.

\*SessionStorage : 로컬스토리지는 브라우저 창을 닫더라도 데이터가 유지되는 반면 세션스토리지는 브라우저가 창을 닫는 순간 영구적으로 데이터를 삭제한다.

<img src="/assets/images/Error/localstorage.png" />

## localStorage 사용방법

```js
// Get
localStorage.getItem("dark-mode");

// Set
localStorage.setItem("dark-mode", true);

// Remove
localStorage.removeItem("dark-mode");

// Remove all keys
localStorage.clear();

// Get n-th key name
localStorage.key(2);
```

## 리액트에서 적용해보기

```js
import * as React from "react";

const App = () => {
  const openLocalStorage =
    typeof window !== "undefined" ? localStorage.getItem("is-open") : null;
  const [isOpen, setOpen] = React.useState(JSON.parse(openLocalStorage));

  const handleToggle = () => {
    localStorage.setItem("is-open", JSON.stringify(!isOpen));

    setOpen(!isOpen);
  };

  return (
    <div>
      <button onClick={handleToggle}>Toggle</button>
      {isOpen && <div>Content</div>}
    </div>
  );
};

export default App;
```

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>context API 사용시 새로고침 및 페이지 이동시에 state가 날아가는 경우 localStorage를 사용한다 </li>
  <li>리액트 유저는 localStorage를 자주 사용하다면 custom Hook 혹은 util, Context API로 만들어 사용하자 </li>
    <li>다만 로컬스토리지는 영구적으로 보관됨으로 중요한 정보가 담겨져있는 경우 SessionStorage를 이용하자 </li>

</ul>
</div>

#### 참조 문서 및 사이트

- [JavaScript LocalStorage 사용 방법과 쿠기와 차이점](https://ponyozzang.tistory.com/341)
- [Local Storage in React](https://www.robinwieruch.de/local-storage-react/)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
