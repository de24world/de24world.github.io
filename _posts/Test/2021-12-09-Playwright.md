---
layout: single
title: "Playwright"
categories: Test
tag: [e2e, Playwright, Testing]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

<img src="/assets/images/CLS/width_height.gif" />

```js
// playwright.config.js
import { PlaywrightTestConfig, devices } from "@playwright/test";

/**
 * 참조 : https://playwright.dev/docs/test-configuration.
 */
const config: PlaywrightTestConfig = {
  testDir: "./e2e/tests",

  /* 한 나의 테스트를 실행할 수 있는 최대시간 - 아래는 30초로 되어있으나 긴 시나리오 테스트의 경우 더 길게 설정하면 된다. 아니면 에러가 발생*/
  timeout: 30 * 1000,

  expect: {
    /**
     * 최대 시간 expect()는 조건이 충족될 때까지 기다려야 합니다.
     * 예를 들어 `await expect(locator).toHaveText();`
     */
    timeout: 5000,
  },

  /* 실수로 소스 코드에 test.only를 남겨둔 경우 CI(Continuous Integration, Git Workflow 등)에서 빌드 실패. */
  forbidOnly: !!process.env.CI,

  /* CI에서만 테스트를 재시도 하려고 할 때 참조 : https://playwright.dev/docs/api/class-testconfig#test-config-retries*/
  retries: process.env.CI ? 1 : 0,

  /* CI에 대한 병렬(parallel) 테스트 옵트아웃. 참조 : https://playwright.dev/docs/api/class-testconfig#test-config-workers */
  workers: process.env.CI ? 1 : 5,

  /* 보고서 사용 방법. 참조 https://playwright.dev/docs/test-reporters */
  reporter: [
    ["list"],
    ["html", { outputFolder: "./e2e/reports/html" }],
    ["json", { outputFile: "./e2e/reports/json/results.json" }],
  ],

  /* 아래의 모든 프로젝트에 대한 공유 설정. 참조 : https://playwright.dev/docs/api/class-testoptions. */
  use: {
    /* `click()`과 같은 각 작업에 소요될 수 있는 최대 시간입니다. 기본값은 0(제한 없음). */
    actionTimeout: 30 * 1000,

    /* `await page.goto('/')` 와 같은 작업에서 사용할 기본 URL. */
    baseURL: "http://localhost:3000/",

    /* 흔적(trace) 수집 옵션. See https://playwright.dev/docs/trace-viewer */
    trace: process.env.CI ? "off" : "on",

    /* https://playwright.dev/docs/test-configuration#automatic-screenshots */
    screenshot: "only-on-failure",
    video: process.env.CI ? undefined : "on",
  },

  /* 주요 브라우저용 프로젝트 구성 */
  projects: [
    {
      name: "chromium",
      testMatch: [/.*all.spec.ts/, /.*desktop.spec.ts/, /.*chrome.spec.ts/],
      /* Project-specific settings. */
      use: {
        ...devices["Desktop Chrome"],
      },
    },

    {
      name: "firefox",
      testMatch: [/.*all.spec.ts/, /.*desktop.spec.ts/],
      use: {
        ...devices["Desktop Firefox"],
      },
    },

    // {
    //   name: 'webkit',
    //   use: {
    //     ...devices['Desktop Safari'],
    //   },
    // },

    /* 모바일 뷰포트에 대한 테스트. */
    {
      name: "Mobile Chrome",
      testMatch: [/.*all.spec.ts/, /.*mobile.spec.ts/],
      use: {
        ...devices["Pixel 4"],
      },
    },
    {
      name: "Mobile Safari",
      testMatch: [/.*all.spec.ts/, /.*mobile.spec.ts/],
      use: {
        ...devices["iPhone 11"],
      },
    },

    /* 브랜드 브라우저에 대한 테스트. */
    // {
    //   name: 'Microsoft Edge',
    //   use: {
    //     channel: 'msedge',
    //   },
    // },
    // {
    //   name: 'Google Chrome',
    //   use: {
    //     channel: 'chrome',
    //   },
    // },
  ],

  /* 스크린샷, 비디오, 추적 등과 같은 테스트 아티팩트를 위한 폴더. */
  outputDir: "./tests/e2e/reports",

  /* 테스트를 시작하기 전에 로컬 개발 서버를 실행하세요. */
  webServer: {
    command: "yarn start",
    port: 3000,
  },
};
export default config;
```

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>Playwright는 Puppeteer와 유사하며 다른 브라우저 선택 가능하고, 다른 언어를 지원한다</li>
  <li>2. </li>
  <li>3. </li>
</ul>
</div>

#### 참고 영상

- [Playwright vs Cypress](https://youtu.be/idX9hSW0MY4){% include video id="idX9hSW0MY4" provider="youtube" %}

#### 참조 문서 및 사이트

- [추천 Udemy 강좌](https://computeruniverse.udemy.com/course/automated-software-testing-with-playwright)
- [Playwright로 E2E 테스트 작성하기](https://ui.toast.com/weekly-pick/ko_20210818)
- [Navigating & waiting](https://www.checklyhq.com/learn/headless/basics-navigation/)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
