---
layout: single
title: "eslint-plugin-import 한국어 번역"
categories: ESLint
tag: [eslint, plugin, import, rules]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

해당 플러그인은 ES2015+(ES6+) 가져오기(import)/내보내기(export) 구문의 린트(Lint)를 지원하고 파일 경로 및 가져오기 이름의 철자 오류 문제를 방지합니다. ES2015+ 정적 모듈 구문이 제공하는 모든 장점들이 편집기에서 표시됩니다.

만약 import 목록들 순서를 보기 좋게 그룹화 및 자동정렬 하고 싶다면 꼭 사용하기를 추천한다.

## 설치방법

```sh
npm install eslint-plugin-import -g
```

혹은 ESLint을 dev(개발) dependency(종속성) 관리하고 싶다면:

```sh
# 프로젝트의 작업 트리 내부
npm install eslint-plugin-import --save-dev
```

모든 규칙들은 기본적으로 해제되어있습니다. 단, 당신의 `.eslintrc.(yml|json|js)` 파일에서 수동으로 구성을 설정할 수 있습니다.

```yaml
---
extends:
  - eslint:recommended
  - plugin:import/recommended
  # 또는, 'recommended' 는 다음 두 규칙 집합의 조합입니다:
  - plugin:import/errors
  - plugin:import/warnings

# 혹은 수동으로 설정하세요:
plugins:
  - import

rules:
  import/no-unresolved: [2, { commonjs: true, amd: true }]
  import/named: 2
  import/namespace: 2
  import/default: 2
  import/export: 2
  # 그외...
```

# TypeScript

다음 단축키를 사용하거나 아래에 설명된 세부 설정을 사용하여 고유한 조합을 설정할 수 있습니다.
[`@typescript-eslint/parser`] 가 당신의 구성에서 설치가 되어있는지 확인하세요. 불행하게도 NPM은 선택정으로 종속성을 나열 할 수 없습니다.

```yaml
extends:
  - eslint:recommended
  - plugin:import/recommended
  - plugin:import/typescript # 해당 라인은 속임수입니다.
```

[`@typescript-eslint/parser`]: https://github.com/typescript-eslint/typescript-eslint/tree/HEAD/packages/parser

또한 Typescript resolver를 설치하고 구성해야 합니다.
[`eslint-import-resolver-typescript`](https://github.com/alexgorbatchev/eslint-import-resolver-typescript).

# import/order: 모듈(module) 가져오기(import) 순서(order) 규칙 적용하기

`require()` / `import` 구문을 사용하여 순서 규칙을 적용합니다. +(수정가능) [명령어 라인(command line)]에서 `--fix` 옵션은 보고된 문제들을 자동적으로 수정합니다.

[`groups`](#groups-array) 의 `["builtin", "external", "internal", "parent", "sibling", "index", "object", "type"]`로 된 설정은 다음 예제의 순서와 같습니다.

```js
// 1. 노드 "builtin" 모듈
import fs from 'fs';
import path from 'path';
// 2. "외부(external)" 모듈
import _ from 'lodash';
import chalk from 'chalk';
// 3. "내부(internal)" modules
// (내부 경로를 다르게 처리하도록 경로 또는 웹팩을 구성한 경우)
import foo from 'src/foo';
// 4. "상위(부모, parent)" 디렉토리 모듈
import foo from '../foo';
import qux from '../../foo/qux';
// 5. 동일하거나 "형제(sibling)"  디렉토리 모듈
import bar from './bar';
import baz from './bar/baz';
// 6. "index" 현재 디렉토리
import main from './';
// 7. "object"-imports (오직 TypeScript에서만 사용 가능합니다)
import log = console.log;
// 8. "type" imports (오직 Flow 이나 TypeScript에서 사용 가능합니다)
import type { Foo } from 'foo';
```

할당되지 않은 import(가져오기)들은 가져오는 순서가 중요할 수 있으므로 무시됩니다. ES6 `import` 구문은 반드시 `require()` 구문 앞에 써야합니다.

## 틀린 경우(Fail)

```js
import _ from "lodash";
import path from "path"; // `path` 는 `lodash` 이전에 반드시 import 해야합니다.

// -----

var _ = require("lodash");
var path = require("path"); // `path` 는 `lodash` 이전에 반드시 import 해야합니다.

// -----

var path = require("path");
import foo from "./foo"; // `import` 는 `require` 이전에 써야합니다.
```

## 맞는 경우(Pass)

```js
import path from "path";
import _ from "lodash";

// -----

var path = require("path");
var _ = require("lodash");

// -----

//  ̀`babel-register` 가 먼저 사용해야합니다.
require("babel-register");
var path = require("path");

// -----

// `import` 는 `require` 이전에 사용해야 합니다.
import foo from "./foo";
var path = require("path");
```

## Options

This rule supports the following options:

### `groups: [array]`:

How groups are defined, and the order to respect. `groups` must be an array of `string` or [`string`]. The only allowed `string`s are:
`"builtin"`, `"external"`, `"internal"`, `"unknown"`, `"parent"`, `"sibling"`, `"index"`, `"object"`, `"type"`.
The enforced order is the same as the order of each element in a group. Omitted types are implicitly grouped together as the last element. Example:

```js
[
  "builtin", // Built-in types are first
  ["sibling", "parent"], // Then sibling and parent types. They can be mingled together
  "index", // Then the index file
  "object",
  // Then the rest: internal and external type
];
```

The default value is `["builtin", "external", "parent", "sibling", "index"]`.

You can set the options like this:

```js
"import/order": ["error", {"groups": ["index", "sibling", "parent", "internal", "external", "builtin", "object", "type"]}]
```

### `pathGroups: [array of objects]`:

To be able to group by paths mostly needed with aliases pathGroups can be defined.

Properties of the objects

| property       | required | type   | description                                                                                                                                              |
| -------------- | :------: | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| pattern        |    x     | string | minimatch pattern for the paths to be in this group (will not be used for builtins or externals)                                                         |
| patternOptions |          | object | options for minimatch, default: { nocomment: true }                                                                                                      |
| group          |    x     | string | one of the allowed groups, the pathGroup will be positioned relative to this group                                                                       |
| position       |          | string | defines where around the group the pathGroup will be positioned, can be 'after' or 'before', if not provided pathGroup will be positioned like the group |

```json
{
  "import/order": [
    "error",
    {
      "pathGroups": [
        {
          "pattern": "~/**",
          "group": "external"
        }
      ]
    }
  ]
}
```

### `pathGroupsExcludedImportTypes: [array]`:

This defines import types that are not handled by configured pathGroups.
This is mostly needed when you want to handle path groups that look like external imports.

Example:

```json
{
  "import/order": [
    "error",
    {
      "pathGroups": [
        {
          "pattern": "@app/**",
          "group": "external",
          "position": "after"
        }
      ],
      "pathGroupsExcludedImportTypes": ["builtin"]
    }
  ]
}
```

You can also use `patterns`(e.g., `react`, `react-router-dom`, etc).

Example:

```json
{
  "import/order": [
    "error",
    {
      "pathGroups": [
        {
          "pattern": "react",
          "group": "builtin",
          "position": "before"
        }
      ],
      "pathGroupsExcludedImportTypes": ["react"]
    }
  ]
}
```

The default value is `["builtin", "external"]`.

### `newlines-between: [ignore|always|always-and-inside-groups|never]`:

Enforces or forbids new lines between import groups:

- If set to `ignore`, no errors related to new lines between import groups will be reported (default).
- If set to `always`, at least one new line between each group will be enforced, and new lines inside a group will be forbidden. To prevent multiple lines between imports, core `no-multiple-empty-lines` rule can be used.
- If set to `always-and-inside-groups`, it will act like `always` except newlines are allowed inside import groups.
- If set to `never`, no new lines are allowed in the entire import section.

With the default group setting, the following will be invalid:

```js
/* eslint import/order: ["error", {"newlines-between": "always"}] */
import fs from "fs";
import path from "path";
import index from "./";
import sibling from "./foo";
```

```js
/* eslint import/order: ["error", {"newlines-between": "always-and-inside-groups"}] */
import fs from "fs";

import path from "path";
import index from "./";
import sibling from "./foo";
```

```js
/* eslint import/order: ["error", {"newlines-between": "never"}] */
import fs from "fs";
import path from "path";

import index from "./";

import sibling from "./foo";
```

while those will be valid:

```js
/* eslint import/order: ["error", {"newlines-between": "always"}] */
import fs from "fs";
import path from "path";

import index from "./";

import sibling from "./foo";
```

```js
/* eslint import/order: ["error", {"newlines-between": "always-and-inside-groups"}] */
import fs from "fs";

import path from "path";

import index from "./";

import sibling from "./foo";
```

```js
/* eslint import/order: ["error", {"newlines-between": "never"}] */
import fs from "fs";
import path from "path";
import index from "./";
import sibling from "./foo";
```

### `alphabetize: {order: asc|desc|ignore, caseInsensitive: true|false}`:

Sort the order within each group in alphabetical manner based on **import path**:

- `order`: use `asc` to sort in ascending order, and `desc` to sort in descending order (default: `ignore`).
- `caseInsensitive`: use `true` to ignore case, and `false` to consider case (default: `false`).

Example setting:

```js
alphabetize: {
  order: 'asc', /* sort in ascending order. Options: ['ignore', 'asc', 'desc'] */
  caseInsensitive: true /* ignore case. Options: [true, false] */
}
```

This will fail the rule check:

```js
/* eslint import/order: ["error", {"alphabetize": {"order": "asc", "caseInsensitive": true}}] */
import React, { PureComponent } from "react";
import aTypes from "prop-types";
import { compose, apply } from "xcompose";
import * as classnames from "classnames";
import blist from "BList";
```

While this will pass:

```js
/* eslint import/order: ["error", {"alphabetize": {"order": "asc", "caseInsensitive": true}}] */
import blist from "BList";
import * as classnames from "classnames";
import aTypes from "prop-types";
import React, { PureComponent } from "react";
import { compose, apply } from "xcompose";
```

### `warnOnUnassignedImports: true|false`:

- default: `false`

Warns when unassigned imports are out of order. These warning will not be fixed
with `--fix` because unassigned imports are used for side-effects and changing the
import of order of modules with side effects can not be done automatically in a
way that is safe.

This will fail the rule check:

```js
/* eslint import/order: ["error", {"warnOnUnassignedImports": true}] */
import fs from "fs";
import "./styles.css";
import path from "path";
```

While this will pass:

```js
/* eslint import/order: ["error", {"warnOnUnassignedImports": true}] */
import fs from "fs";
import path from "path";
import "./styles.css";
```

## Related

- [`import/external-module-folders`] setting

- [`import/internal-regex`] setting

[`import/external-module-folders`]: ../../README.md#importexternal-module-folders
[`import/internal-regex`]: ../../README.md#importinternal-regex

## 개인 적용예시

### `.eslintrc.js` 설정 예시

```javascript
// .eslintrc.js
module.exports = {
  extends: ["next", "prettier"],
  rules: {
    "import/order": [
      "error",
      {
        groups: ["builtin", "external", "parent", "sibling", "index", "object"],
        pathGroups: [
          {
            pattern: "~/**",
            group: "external",
            position: "before",
          },
          { pattern: "@*", group: "external", position: "after" },
          { pattern: "@*/**", group: "external", position: "after" },
        ],
        pathGroupsExcludedImportTypes: ["react"],
        "newlines-between": "always",
        alphabetize: {
          order: "asc",
          caseInsensitive: true,
        },
      },
    ],
  },
};
```

### 파일 적용 후

```javascript
// 적용 후
import React from "react";
import { connect } from "react-redux";

import CustomerModel from "@Components/Api/Customer/Models/CustomerModel";
import ErrorsModel from "@Components/Api/Error/Model/ErrorsModel";
import { trackException } from "@Components/ApplicationInsights";
import CustomerNavigation from "@Components/Customer/Components/CustomerNavigation/CustomerNavigation";
import { getGlobalDYCampaignChoiceResponse } from "@Components/DY/Api/utils";
import ApiDownExceptionModel from "@Components/ErrorTemplates/ApiDownExceptionModel";
import PageNotFound from "@Components/ErrorTemplates/PageNotFound";
import Layout from "@Components/Layout/Layout";
import MetaFormatter from "@Components/Meta/MetaFormatter";
import Service from "@Components/Service/Service";
import Topic from "@Components/Topic/Topic";
import TopicApi from "@Components/Topic/TopicApi";
import TopicModel from "@Components/Topic/TopicModel";
import { getDYChoiceResponseForTopic } from "@Components/Topic/TopicUtils";
import ApiStatus from "@Enum/ApiStatus";
import CustomerStatus from "@Enum/CustomerStatus";
import PageContextType from "@Enum/PageContextType";
import PageType from "@Enum/Pagetype";

import TopicPageInterface from "../../pageInterfaces/TopicPageInterface";
import { getServerSideProps as MainGetServerSideProps } from "../../src/MainPage";
import { wrapper } from "../../src/store/Store";
```

## 요약

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li>1. </li>
  <li> 자세한 설정은 공식문서를 참조하자</li>
  <li>3. </li>
</ul>
</div>

#### 참고 영상

- [Import eslint plugin (My eslint config part 4)](https://youtu.be/d6Xa87sObGo){% include video id="d6Xa87sObGo" provider="youtube" %}

#### 참조 문서 및 사이트

- [eslint-plugin-import.md](https://github.com/import-js/eslint-plugin-import/blob/main/README.md)
- [eslint-plugin-import.md 규칙 문서](https://github.com/import-js/eslint-plugin-import/blob/main/docs/rules/order.md)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
