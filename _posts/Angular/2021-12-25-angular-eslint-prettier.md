---
layout: single
title: "Angular + Prettier + Eslint"
categories: coding
tag: [angular, prettier, eslint, tslint, lint]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "Angular"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# Eslint 및 Prettier 관련 라이브러리 설치

```
# ESLint 설치
npm install --save-dev eslint

# 추가적인 플러그인들 설치
npm install --save-dev @typescript-eslint/eslint-plugin eslint-plugin-prettier

# Prettier 와 Prettier-ESLint dependencies 설치
npm install --save-dev prettier prettier-eslint eslint-config-prettier
```

- [eslint](https://eslint.org/): ESLint 핵심 린팅(linting) 라이브러리
- [@typescript-eslint/eslint-plugin](https://github.com/typescript-eslint/typescript-eslint): 타입스크립트에 특정한 eslint 규칙을 포함시킨 플러그인
- [prettier](https://prettier.io/): 프리티어(prettier) 핵심 라이브러리
- [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier): prettier와 충돌할 수 있는 Eslint 규칙을 비활성화 시켜줍니다
- [eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier): Prettier를 Eslint 규칙으로 실행시켜줍니다.

# Eslint 파일 설정

```json
.eslintrc
{
  "parser": "@typescript-eslint/parser", // ESLint 파서를 지정합니다.
  "extends": [
    "plugin:@typescript-eslint/recommended", // @typescript-eslint/eslint-plugin의 권장 규칙을 사용합니다.
    "plugin:prettier/recommended" // eslint-plugin-prettier 및 eslint-config-prettier를 활성화합니다. 이것은 ESLint 오류로 prettier 오류를 표시합니다. 이것이 항상 extends 배열의 마지막 구성인지 확인하십시오.
  ],
  "parserOptions": {
    "ecmaVersion": 2020, // 최신 ECMAScript 기능의 구문 분석 허용
    "sourceType": "module" //import 사용 허용을 위해서
  },
  "rules": {
    // ESLint 규칙을 지정하는 위치입니다. 확장 구성에서 지정된 규칙을 덮어쓰는 데 사용할 수 있습니다.
  }
}
```

# .Eslintignore 파일 추가

```json
.eslintignore
예시
package.json
package-lock.json
dist
```

# prettierrc 파일 작성

```json
.prettierrc
{
  "singleQuote": true,
  "trailingComma": "none",
  "endOfLine": "auto"
}
```

# .pakage.json 파일 설정

```json
.package.json
원하시는데로 스크립트를 작성해줍니다
"scripts": {
  "lint": "tsc --noEmit && eslint . --ext js,ts --quiet --fix",
}
```

# 그 외

- 자동저장 및 수정 기능을 위해서는 `setting.json`을 확인해줍니다.`editor.formatONsave` 기능 및 extension 설정 등을 꼭 확인해주세요.

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>관련 라이브러리 설치해줍니다</li>
  <li>eslint 및 prettier 파일을 추가 및 작성해줍니다</li>
  <li>vscode 설정을 확인해줍니다</li>
</ul>
</div>

#### 참조 문서 및 사이트

- [Using ESLint and Prettier with VScode in an Angular Project 🚀(outdated)](https://dev.to/dreiv/using-eslint-and-prettier-with-vscode-in-an-angular-project-42ib)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
