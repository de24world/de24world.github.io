# Next.js Documentation (문서 번역본)

- Updated date 2021.07.19
- next.js 공식 홈페이지 번역본입니다. (https://nextjs.org/docs/)
  까지 반영되어 있습니다.

# 목차

- [시작하며(Getting Started)](#시작하며getting-started)
- [기본 기능(Basic Features)](#기본-기능basic-features)

1.  [페이지들(Pages)](#페이지들pages)
2.  Data Fetching
3.
4.
5.  [이미지 최적화(Image Optimization)](#이미지-최적화image-optimization)

# 시작하며(Getting Started)

Next.js 문서에 오신 것을 환영합니다.
만약 새로운 Next.js가 처음이시라면 해당 [수업](https://nextjs.org/learn/basics/create-nextjs-app)을 먼저 시작하는 것을 추천드립니다.
퀴즈와 함께 다양한 수업들을 통해 당신이 어떻게 Next.js를 사용하는지 알 수 있게 될 것입니다.
Next.js 와 관련된 어떠한 질문이 있다면, Next.js의 커뮤니티에 [Github Discussions](https://github.com/vercel/next.js/discussions) 물어보는 것을 언제든 환영합니다.

#### 시스템 요구사항 (System Reuqirements)

- [Node.js 12](https://nodejs.org/en/) 혹은 그 이상
- MacOS, Windows(WSL 포함), 그리고 Linux 역시 지원합니다.

### 설정(Setup)

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

### 수동 설정(Manual Setup)

`next`, `react` 그리고 `react-dom`을 프로젝트에 설치해주세요

```
npm install next react react-dom
# 혹은
yarn add next react react-dom
```

`package.json`을 열어주시고, `scripts`를 아래와 같이 해주세요:

```
"scripts": {
  "dev": "next dev",
  "build": "next build",
  "start": "next start",
  "lint": "next lint"
}
```

해당 스크립트들은 애플리케이션 개발의 여러 단계를 참조합니다.

- `dev`- `next dev` `개발` 모드에서 Next.js를 시작하는 실행
- `build`- `next build` 프로덕션 사용을 위한 애플리케이션을 `빌드`하는 실행
- `start`- `next start` Next.js `프로덕션 서버를 시작`하는 실행
- `lint`- `next lint` Next.js에 내장된 ESLint 설정을 실행

Next.js는 [페이지](https://nextjs.org/docs/basic-features/pages) 개념을 기반으로 구축되었습니다. A Page는 `pages` 디렉토리에 있는 [React Component](https://reactjs.org/docs/components-and-props.html)로 내보내지는 `.js`, `.jsx`, `.ts`, 또는 `.tsx` 파일입니다.
페이지는 파일 이름에 따라 경로로 연결됩니다. 예를 들어 `pages/about.js`은 `/about` 매핑됩니다. 파일 이름으로 동적 경로 매개변수를 추가할 수도 있습니다.
`pages` 폴더를 프로젝트에 생성해줍니다.
`./pages/index.js`를 일반적으로 다음 내용으로 써줍니다:

```
function HomePage() {
  return <div>Welcome to Next.js!</div>
}

export default HomePage
```

애플리케이션 개발하기 위해서 `npm run dev`또는 `yarn dev` 실행하여 `http://localhost:3000`에서 개발 서버(모드)를 실행합니다.
`http://localhost:3000` 에서 당신의 애플리케이션을 확인할 수 있습니다.

지금까지, 우리는 해당 내용들을 가지고 있습니다.

- 자동 컴파일 및 번들링(webpack 및 babel 포함)
- 리액트의 빠른 새로 고침
- `./pages/`의 정적 생석 혹은 서버 사이드 렌더링
- 정적 파일 제공 . `./public/`는 `/` 매핑됩니다.
  추가적으로, 어떤 Next.js 애플리케이션도 처음부터 프로덕션용(모드)에 사용할 준비가 되어 있습니다 . 자세한 내용은 [배포 문서](https://nextjs.org/docs/deployment) 를 참조 하세요.

**[⬆ 상단으로](#목차)**

# 기본 기능(Basic Features)

# 페이지들(Pages)

> 해당 문서는 Next.js 9.3 이상 버전입니다. 만약 이보다 더 오래된 버전을 사용하고 있다며, [이전 자료](https://nextjs.org/docs/tag/v9.2.2/basic-features/pages)들을 참조하세요

Next.js에서는 a **page**는 `pages` 디렉토리에 있는 [React Component](https://reactjs.org/docs/components-and-props.html)로 내보내지는 `.js`, `.jsx`, `.ts`, 또는 `.tsx` 파일입니다.
예 : 아래와 같이 React component로 내보내지는(export) `pages/about.js`를 생성하였다면, `/about` 접근(액세스)할 수 있습니다.

## 동적 경로 페이지들(Pages with Dynamic Routes)

Next.js는 동적 경로 페이지를 지원합니다. 예를 들어 `pages/posts/[id].js`, 불리는 파일을 만들었다면, `posts/1`, `posts/2` 등에 접근하실 수 있습니다.

> 동적 라우팅에 대해 자세히 알아보려면 [동적 라우팅 문서](https://nextjs.org/docs/routing/dynamic-routes) 확인하세요

# 이미지 최적화(Image Optimization)

[Image Component 예시](https://github.com/vercel/next.js/tree/canary/examples/image-component)

Next.js 의 이미지 컴포넌트인, `next/image`는, HTML의 `<img>`의 최신웹용을 위한 확장판입니다. 여기에는 다양한 퍼포먼스 최적화를 통하여 좋은 [Core Web Vitals](https://nextjs.org/learn/seo/web-performance) 달성하는데 도움을 줍니다. 이 점수들은 당신의 웹사이트를 측정하는데 매우 중요한 요소이며, 그리고 [구글 검색 순위](https://nextjs.org/learn/seo/web-performance/seo-impact)에 반영되기도 합니다.

이미지 컴포넌트는 다음과 같은 몇 가지 최적화 포함하고 있습니다:

- 향상된 성능: 항상 알맞은 이미지 사이지를 각각의 기기에 맞게 제공하며, 모던한 이미지 포맷으로 사용 가능합니다.
- 시각적 안정성: [누적레이아웃 이동(Cumulative Layout Shift)](https://nextjs.org/learn/seo/web-performance/cls)을 자동적으로 방지합니다.
- 더 빠른 페이지 로드 : 뷰포트에 들어갈 때만 이미지들이 불러와지며, 옵션적으로 흘릿하게 표시됩니다.
- 참고 자료(Assset) 유연성: 심지어 원격 서버에 저장된 이미지의 경우에도 이미지 크기 재조정(resizing)을 해줍니다.

## 이미지 Component 사용하기

당신의 어플리케이션에 이미지를 추가하기 위해서는 [next/image](https://nextjs.org/docs/api-reference/next/image) 컴포넌트를 import해주세요

```javascript
import Image from "next/image";
```

이제 이미지(local 혹은 remote)의 `src` 정의해주세요.

### Local 이미지

`.jpg`, `.png` 또는 `.webp` 로컬 이미지 파일을 import해주세요

```javascirpt
import profilePic from '../public/me.png'
```

동적으로 `await import()` 또는 `require()`는 지원하지 않습니다. `import`는 반드시 빌드시에 분석하기 위해서 정적이여야합니다.

Next.js는 가져온 파일에 따라 이미지의 `넓이(width)`와 `높이(height)`를 자동적으로 결정합니다. 이 값은 이미지를 로드하는동안 [Cumulative Layout Shift(레이아웃 이동)](https://nextjs.org/learn/seo/web-performance/cls)

```javascript
import Image from "next/image";
import profilePic from "../public/me.png";

function Home() {
  return (
    <>
      <h1>My Homepage</h1>
      <Image
        src={profilePic}
        alt="Picture of the author"
        // width={500} automatically provided (자동적으로 제공)
        // height={500} automatically provided (자동적으로 제공)
        // blurDataURL="data:..." automatically provided (자동적으로 제공)
        // placeholder="blur" // Optional blur-up while loading(로딩되는 동안 옵션으로 모자이크 처리)
      />
      <p>Welcome to my homepage!</p>
    </>
  );
}
```

### 원격(Remote) 이미지

원격 이미지를 사용하기 위해서는, `src` 속성이 URL [상대경로](https://nextjs.org/docs/basic-features/image-optimization#loaders) 혹은 [절대경로](https://nextjs.org/docs/basic-features/image-optimization#domains)인 문자열이여야 합니다. 왜냐하면 Next.js는 빌드 프로세스 중에 원격 파일을 접근(access) 할 수 없기 때문에, `[넓이](https://nextjs.org/docs/api-reference/next/image#width)`, `[높이](https://nextjs.org/docs/api-reference/next/image#height)` 그리고 `[blurDataURL](https://nextjs.org/docs/api-reference/next/image#blurdataurl) props 일일이 입력해주어야 합니다.

```javascript
import Image from "next/image";

export default function Home() {
  return (
    <>
      <h1>My Homepage</h1>
      <Image
        src="/me.png"
        alt="Picture of the author"
        width={500}
        height={500}
      />
      <p>Welcome to my homepage!</p>
    </>
  );
}
```

`next/image`의 [사이즈 요구사항](https://nextjs.org/docs/basic-features/image-optimization#image-sizing)에 대해서 더 알아보세요.

### 도메인

원격 이미지를 사용하려는 경우도 있지만, Next.js 내장 이미지 최적화 API를 계속 사용하세요. 이렇게 하려면, 로더(`loader`)로 기본 설정을 유지하고, 이미지 `src` URL 절대경로를 입력하세요.

악의적인 사용자로부터 응용 프로그램을 보호하려면 이러한 방식으로 이러한 방식으로 접근(access)하려는 원격 도메인 목록을 정의해야합니다. 이것은 아래와 같이 `next.config.js`파일에서 구성해주어야 합니다 :

```javascript
module.exports = {
  images: {
    domains: ["example.com", "example2.com"],
  },
};
```

### 로더(Loaders)

앞의 예에서는 원격 이미지를 위한 대한 부분 URL (`"/me.png`)이 제공됩니다. 이는 `next/imag` [lodaer](https://nextjs.org/docs/api-reference/next/image#loader) 아키텍처 때문에 가능한 것입니다.

로더는 이미지에 대한 URL을 생성하는 기능입니다. 제공된 `src`에 루트(root) 도메인을 추가하고 여러 URL을 생성하여 다른 크기의 이미지를 요청합니다. 이러한 여러 URL은 자동 [srcset](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/srcset) 생성에 사용됨으로 사이트를 방문하는 방문객에게 뷰포트에 적합한 크기의 이미지를 제공합니다.

Next.js 응용 프로그램의 기본 로더는 내장된 이미지 최적화 API 를 사용하여 웹의 모든 위치에서 이미지를 최적화 한 다음, NExt.js 웹 서버에 직접 이미지를 제공합니다. CDN이나 이미지 서버에서 직접 이미지를 서비스하려면 [내장된 로더들](https://nextjs.org/docs/api-reference/next/image#built-in-loaders) 중 하나를 사용하거나 몇 줄의 자바스크립트를 직접 작성하시면 됩니다.rom a CDN or image server, you can use one of the built-in loaders or write your own with a few lines of JavaScript.

로더들은 이미지마다 정의할 수 있거나, 혹은 어플맄이션 레벨에 따라 정의될 수 있습니다.

### 우선순위(Priority)

각각의 페이지의 [Largest Contentful Paint (LCP) element](https://web.dev/lcp/#what-elements-are-considered) 위해서 이미지에 `우선순위(priority)` 속성을 추가해야 합니다. 이렇게 하면 Next.js가 로딩을 위해서(예: 태그를 미리 로드하거나 힌트들을 우선하여) 이미지의 우선 순위를 특별히 지정할 수 있어, LCP 점수를 증가시킬 수 있도록 해줍니다.

LCP element(요소)들은 페이지 내의 뷰포트에서 보이는 특별히 가장 큰 이미지 혹은 텍스트 블록입니다. 만약 당신이 `next dev` 실행시킨다면, `<Image>` `우선순위(priority)` 속성이 없는 LCP element들을 콘솔 경고창(console warning)에서 볼 수 있습니다.

LCP 이미지를 식별했다면, 아래와 같이 속성을 추가할 수 있습니다:

```javascript
import Image from "next/image";

export default function Home() {
  return (
    <>
      <h1>My Homepage</h1>
      <Image
        src="/me.png"
        alt="Picture of the author"
        width={500}
        height={500}
        priority
      />
      <p>Welcome to my homepage!</p>
    </>
  );
}
```

속성에 대한 자세한 사항은 [`next/image` 컴포넌트 문서](https://nextjs.org/docs/api-reference/next/image#priority)에서 확인하세요.

### Image Sizing

One of the ways that images most commonly hurt performance is through layout shift, where the image pushes other elements around on the page as it loads in. This performance problem is so annoying to users that it has its own Core Web Vital, called Cumulative Layout Shift. The way to avoid image-based layout shifts is to always size your images. This allows the browser to reserve precisely enough space for the image before it loads.

Because next/image is designed to guarantee good performance results, it cannot be used in a way that will contribute to layout shift, and must be sized in one of three ways:

Automatically, using a static import
Explicitly, by including a height and width property
Implicitly, by using layout="fill" which causes the image to expand to fill its parent element.
What if I don't know the size of my images?
If you are accessing images from a source without knowledge of the images' sizes, there are several things you can do:

Use layout='fill'

The fill layout mode allows your image to be sized by its parent element. Consider using CSS to give the image's parent element space on the page, then using the objectFit property with fill, contain, or cover, along with the objectPosition property to define how the image should occupy that space.

Normalize your images

If you're serving images from a source that you control, consider modifying your image pipeline to normalize the images to a specific size.

Modify your API calls

If your application is retrieving image URLs using an API call (such as to a CMS), you may be able to modify the API call to return the image dimensions along with the URL.

If none of the suggested methods works for sizing your images, the next/image component is designed to work well on a page alongside standard <img> elements.

Styling
Styling the Image component is not that different from styling a normal <img> element, but there are a few guidelines to keep in mind:

Pick the correct layout mode

The image component has several different layout modes that define how it is sized on the page. If the styling of your image isn't turning out the way you want, consider experimenting with other layout modes.

Target the image with className, not based on DOM structure

Regardless of the layout mode used, the Image component will have a consistent DOM structure of one <img> tag wrapped by exactly one <span>. For some modes, it may also have a sibling <span> for spacing. These additional <span> elements are critical to allow the component to prevent layout shifts.

The recommended way to style the inner <img> is to set the className prop on the Image component to the value of an imported CSS Module. The value of className will be automatically applied to the underlying <img> element.

Alternatively, you can import a global stylesheet and manually set the className prop to the same name used in the global stylesheet.

You cannot use styled-jsx because its scoped to the current component.

You cannot use the style prop because the <Image> component does not pass it through to the underlying <img>.

When using layout='fill', the parent element must have position: relative

This is necessary for the proper rendering of the image element in that layout mode.

When using layout='responsive', the parent element must have display: block

This is the default for <div> elements but should be specified otherwise.

Properties
View all properties available to the next/image component.

Styling Examples
For examples of the Image component used with the various fill modes, see the Image component example app.

Configuration
The next/image component and Next.js Image Optimization API can be configured in the next.config.js file. These configurations allow you to enable remote domains, define custom image breakpoints, change caching behavior and more.

Read the full image configuration documentation for more information.

Related
For more information on what to do next, we recommend the following sections:

next/image
See all available properties for the Image component

## ○ 참고 영상

- [왜 Recoil을 써야하는가?](https://youtu.be/H10KNVxF6_s)
- [ARIA에 대해서 HTML 접근성 향상시키기](https://youtu.be/MQHNTzdqet0)

## ○ 참조 문서 및 사이트

- [리액트 상태 관리 가이드](https://www.stevy.dev/react-state-management-guide)
- [리덕스 잘 쓰고 계시나요?](https://ridicorp.com/story/how-to-use-redux-in-ridi/)
- [웹 폰트 사용과 최적화의 최근 동향](https://d2.naver.com/helloworld/4969726)
- [](https://uploadcare.com/blog/next-js-image-optimization/)
