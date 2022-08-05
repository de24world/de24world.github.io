---
layout: single
title: "useEffect와 useState state 업데이트 에러"
categories: Error
tag:
  [
    리액트,
    react,
    useState,
    useEffect,
    Update,
    Error,
    리렌더링,
    rerender,
    에러,
    업데이트,
    페이지,
    새로고침,
    초기값,
    상태,
  ]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# 에러

증상은 페이지 이동시에는 새로 고침하면 API가 새로 호출되어 화면이 리렌더링 되고 있었으나, 뒤로가기 통해서 다시 해당 페이지 들어가면 리렌더링이 제대로 되지 않았다. `debugger`를 통한 디버깅해보니 state값이 제대로 변경되지 않고 있었다. 즉, 컴포넌트 리렌더링시 props 값은 변경되고 있으나, useEffect를 통한 state가 변경되고 있지 않았다. 비슷한 증상 stackoverflow 검색 내용을 첨부하니 참조하자.

```tsx
import React, { useState, useEffect } from "react";
import { Route, Redirect } from "react-router-dom";
import { checkLoggedIn } from "utils/Api";

export const Auth = (props) => {
  const [currentUser, setCurrentUser] = useState(null);
  const [isLoading, setIsLoading] = useState(false);
  console.log(currentUser);

  useEffect(() => {
    const f = async () => {
      setIsLoading(true);
      console.log(isLoading);
      const res = await checkLoggedIn();
      if (!!res) {
        // ==> true
        setCurrentUser(res);
        console.log(currentUser); // ==> null!
      }
      setIsLoading(false);
    };
    f();
  });

  if (isLoading) {
    return <div>loading</div>;
  }

  console.log(currentUser); // ==> null!
  return !!currentUser ? (
    <Route children={props.children} />
  ) : (
    <Redirect to={"/login"} />
  );
};
```

# 해결방법

리액트에서 리렌더링은 보통 **1. 부모 컴포넌트가 리렌더링 될 때** / **2.props가 바뀔 때** / **3.state 값이 바뀔 때** 이루어진다. 리렌더링이 제대로 이루어지지 않고 있다면 위의 3가지 값들을 디버깅해보자. 필자의 경우 **props 값은 제대로 변경되고 있었으나 state 값이 제대로 변경되지 않았다**. 그래서 stackoverflow에서 검색하여 해결해보니 **`useState()`의 초기값이 타입(예:array, object 등)이 일치하지 않았다**. 예를 들어 필자는 State 값에 Arrary(배열) 값이 할당되고 있었으나 **useState()로 초기값이 할당되어있었다**. 따라서 **useState([])** 로 변경하니 정상적으로 리렌더링이 이루어졌다. 아래의 경우는 state 값에 `Object{}`가 할당된 경우이니 참조하자.

```tsx
const [currentUser, setCurrentUser] = useState(null);
// 위의 코드를

const [currentUser, setCurrentUser] = useState({});
// 해당 코드로 변경해보자
```

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>리렌더링이 제대로 되지 않는다면, props, state, 부모컴포넌트를 체크해보자</li>
  <li>state가 제대로 변경되지 않았다면 state 초기값의 타입을 체크해보자</li>
</ul>
</div>

#### 참조 문서 및 사이트

- [useState in useEffect does not update state](https://stackoverflow.com/questions/64191896/usestate-in-useeffect-does-not-update-state)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
