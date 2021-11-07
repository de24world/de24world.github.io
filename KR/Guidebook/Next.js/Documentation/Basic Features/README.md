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

## 페이지들(Pages)

> 해당 문서는 Next.js 9.3 이상 버전입니다. 만약 이보다 더 오래된 버전을 사용하고 있다며, [이전 자료](https://nextjs.org/docs/tag/v9.2.2/basic-features/pages)들을 참조하세요

Next.js에서는 a **page**는 `pages` 디렉토리에 있는 [React Component](https://reactjs.org/docs/components-and-props.html)로 내보내지는 `.js`, `.jsx`, `.ts`, 또는 `.tsx` 파일입니다.
예 : 아래와 같이 React component로 내보내지는(export) `pages/about.js`를 생성하였다면, `/about` 접근(액세스)할 수 있습니다.

### 동적 경로 페이지들(Pages with Dynamic Routes)

Next.js는 동적 경로 페이지를 지원합니다. 예를 들어 `pages/posts/[id].js`, 불리는 파일을 만들었다면, `posts/1`, `posts/2` 등에 접근하실 수 있습니다.

> 동적 라우팅에 대해 자세히 알아보려면 [동적 라우팅 문서](https://nextjs.org/docs/routing/dynamic-routes) 확인하세요

## 이미지 최적화(Image Optimization)

[Image Component 예시](https://github.com/vercel/next.js/tree/canary/examples/image-component)

Next.js 의 이미지 컴포넌트인, `next/image`는, HTML의 `<img>`의 최신웹용을 위한 확장판입니다. 여기에는 다양한 퍼포먼스 최적화를 통하여 좋은 [Core Web Vitals](https://nextjs.org/learn/seo/web-performance) 달성하는데 도움을 줍니다. 이 점수들은 당신의 웹사이트를 측정하는데 매우 중요한 요소이며, 그리고 [구글 검색 순위](https://nextjs.org/learn/seo/web-performance/seo-impact)에 반영되기도 합니다.

These scores are an important measurement of user experience on your website, and are factored into Google's search rankings.

Some of the optimizations built into the Image component include:

Improved Performance: Always serve correctly sized image for each device, using modern image formats.
Visual Stability: Prevent Cumulative Layout Shift automatically.
Faster Page Loads: Images are only loaded when they enter the viewport, with optional blur-up placeholders
Asset Flexibility: On-demand image resizing, even for images stored on remote servers
Using the Image Component
To add an image to your application, import the next/image component:

import Image from 'next/image'
Now, you can define the src for your image (either local or remote).

Local Images
To use a local image, import your .jpg, .png, or .webp files:

import profilePic from '../public/me.png'
Dynamic await import() or require() are not supported. The import must be static so it can be analyzed at build time.

Next.js will automatically determine the width and height of your image based on the imported file. These values are used to prevent Cumulative Layout Shift while your image is loading.

import Image from 'next/image'
import profilePic from '../public/me.png'

function Home() {
return (
<>
<h1>My Homepage</h1>
<Image
src={profilePic}
alt="Picture of the author"
// width={500} automatically provided
// height={500} automatically provided
// blurDataURL="data:..." automatically provided
// placeholder="blur" // Optional blur-up while loading
/>
<p>Welcome to my homepage!</p>
</>
)
}
Remote Images
To use a remote image, the src property should be a URL string, which can be relative or absolute. Because Next.js does not have access to remote files during the build process, you'll need to provide the width, height and optional blurDataURL props manually:

import Image from 'next/image'

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
)
}
Learn more about the sizing requirements in next/image.

Domains
Sometimes you may want to access a remote image, but still use the built-in Next.js Image Optimization API. To do this, leave the loader at its default setting and enter an absolute URL for the Image src.

To protect your application from malicious users, you must define a list of remote domains that you intend to access this way. This is configured in your next.config.js file, as shown below:

module.exports = {
images: {
domains: ['example.com', 'example2.com'],
},
}
Loaders
Note that in the example earlier, a partial URL ("/me.png") is provided for a remote image. This is possible because of the next/image loader architecture.

A loader is a function that generates the URLs for your image. It appends a root domain to your provided src, and generates multiple URLs to request the image at different sizes. These multiple URLs are used in the automatic srcset generation, so that visitors to your site will be served an image that is the right size for their viewport.

The default loader for Next.js applications uses the built-in Image Optimization API, which optimizes images from anywhere on the web, and then serves them directly from the Next.js web server. If you would like to serve your images directly from a CDN or image server, you can use one of the built-in loaders or write your own with a few lines of JavaScript.

Loaders can be defined per-image, or at the application level.

Priority
You should add the priority property to the image that will be the Largest Contentful Paint (LCP) element for each page. Doing so allows Next.js to specially prioritize the image for loading (e.g. through preload tags or priority hints), leading to a meaningful boost in LCP.

The LCP element is typically the largest image or text block visible within the viewport of the page. When you run next dev, you'll see a console warning if the LCP element is an <Image> without the priority property.

Once you've identified the LCP image, you can add the property like this:

import Image from 'next/image'

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
)
}
See more about priority in the next/image component documentation.

Image Sizing
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
