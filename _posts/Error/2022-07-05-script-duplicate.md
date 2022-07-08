---
layout: single
title: "외부 script 중복 생성 문제 window reset으로 해결하기"
categories: Error
tag:
  [
    script,
    중복,
    error,
    에러,
    reset,
    리셋,
    window,
    스크립트,
    윈도우,
    flixmedia,
    리액트,
    react,
  ]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# 문제

현재 리액트 앱(Next.js)에서 useEffect를 이용해서 외부에서 스크립트를 불러와서 쓰고 있다. 그런데 `return () => { const s = document.getElementById("inlineContent-flixMedia"); s.parentElement.removeChild(s);}` cleanup 함수로 변환했음에도 불구하고 컴포넌트를 리렌더링 하였을 때, 스크립트가 두번 생성되는 에러가 발생하였다

<img src="/assets/images/Error/script-duplicate.png" />

외부 스크립트(flixmedia) : 해당 스크립트는 물건 상세설명 이미지를 만들어주는 스크립트이다  
https://www.flixmedia.com/flix-solutions/retailer/faqs

<img src="/assets/images/Error/flixmedia.png" />

```js
useEffect(() => {
  const s = document.createElement("script");
  s.id = "inlineContent-flixMedia";
  s.type = "text/javascript";
  s.src = AppConfig.NEXT_PUBLIC_INLINE_CDN_FLIXMEDIA_SCRIPT;
  s.async = true;
  s.setAttribute("data-flix-distributor", { distributor_id });
  s.setAttribute("data-flix-language", "{language_code}");
  s.setAttribute("data-flix-brand", "{brand_name}");
  s.setAttribute("data-flix-mpn", "{mpn}");
  s.setAttribute("data-flix-ean", "{ean}");
  s.setAttribute("data-flix-sku", "");
  s.setAttribute("data-flix-button", "flix-minisite");
  s.setAttribute("data-flix-inpage", "flix-inpage");
  s.setAttribute("data-flix-button-image", "");
  s.setAttribute("data-flix-fallback-language", "");
  s.setAttribute("data-flix-price", "");
  document.head.insertBefore(
    s,
    document.head.getElementsByTagName("script")[0]
  );

  return () => {
    const s = document.getElementById("inlineContent-flixMedia");
    s.parentElement.removeChild(s);
  };
}, []);
return <div id="flix-inpage" />;
```

# 해결

결론은 `window`의 `reset()` 전역 함수를 이용한다. `flixJsCallbacks` 는 window 이벤트를 명명하기 위해서 붙였을 뿐, 별 의미는 없다. `(typeof window !== undefined)` 는 정의되지 않은 window의 타입이기 때문에 `undefied`가 발생해도 에러가 발생하지 않게 해준다

````js
    useEffect(() => {
        // 아래의 window 이벤트를 추가해준다.
        if (
            typeof (window as any).flixJsCallbacks === 'object' &&
            typeof (window as any).flixJsCallbacks.reset != 'undefined'
        ) {
            (window as any).flixJsCallbacks?.reset();
        }

        const s = document.createElement('script');
        s.id = 'inlineContent-flixMedia';
        s.type = 'text/javascript';
        ...
        }

        return () => {
            const flixScript = document.getElementById('inlineContent-flixMedia');
            flixScript.parentElement.removeChild(s);
        };
    }, []);
    return <div id="flix-inpage" />;
    ```


````
