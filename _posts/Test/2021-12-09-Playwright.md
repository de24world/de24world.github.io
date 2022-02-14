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

  /* Fail the build on CI if you accidentally left test.only in the source code. */
  forbidOnly: !!process.env.CI,

  /* Retry on CI only */
  retries: process.env.CI ? 1 : 0,

  /* Opt out of parallel tests on CI. */
  workers: process.env.CI ? 1 : undefined,

  /* Reporter to use. See https://playwright.dev/docs/test-reporters */
  reporter: [
    ["list"],
    ["html", { outputFolder: "./e2e/reports/html" }],
    ["json", { outputFile: "./e2e/reports/json/results.json" }],
  ],

  /* Shared settings for all the projects below. See https://playwright.dev/docs/api/class-testoptions. */
  use: {
    /* Maximum time each action such as `click()` can take. Defaults to 0 (no limit). */
    actionTimeout: 30 * 1000,

    /* Base URL to use in actions like `await page.goto('/')`. */
    baseURL: "http://localhost:3000/",

    /* Collect trace when retrying the failed test. See https://playwright.dev/docs/trace-viewer */
    trace: "on-first-retry",

    /* https://playwright.dev/docs/test-configuration#automatic-screenshots */
    screenshot: "only-on-failure",
    video: process.env.CI ? undefined : "on",
  },

  /* Configure projects for major browsers */
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

    /* Test against mobile viewports. */
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

    /* Test against branded browsers. */
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

  /* Folder for test artifacts such as screenshots, videos, traces, etc. */
  outputDir: "./tests/e2e/reports",

  /* Run your local dev server before starting the tests */
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
  <li>1. </li>
  <li>2. </li>
  <li>3. </li>
</ul>
</div>

#### 참고 영상

- [Playwright vs Cypress](https://youtu.be/idX9hSW0MY4){% include video id="idX9hSW0MY4" provider="youtube" %}

#### 참조 문서 및 사이트

- [추천 Udemy 강좌](https://computeruniverse.udemy.com/course/automated-software-testing-with-playwright)
- [Playwright로 E2E 테스트 작성하기](https://ui.toast.com/weekly-pick/ko_20210818)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
