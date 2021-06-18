# clean-code-javascript

* Updated date 2020.01.09
* 현재 원문의 [1c0b20a](https://github.com/ryanmcdermott/clean-code-javascript/commit/1c0b20a91eb2efe529760eaa6cc4c9cc21daf547)
까지 반영되어 있습니다.

## 목차
  1. [소개(Introduction)](#소개introduction)
  2. [변수(Variables)](#변수variables)
  3. [함수(Functions)](#함수functions)
  4. [객체와 자료구조(Objects and Data Structures)](#객체와-자료구조objects-and-data-structures)
  5. [클래스(Classes)](#클래스classes)
  6. [SOLID](#SOLID)
  7. [테스트(Testing)](#테스트testing)
  8. [동시성(Concurrency)](#동시성concurrency)
  9. [에러 처리(Error Handling)](#에러-처리error-handling)
 10. [포맷팅(Formatting)](#포맷팅formatting)
 11. [주석(Comments)](#주석comments)
 12. [번역(Translation)](#번역translation)

## 소개(Introduction)
![코드를 읽을 때 소리 지르는 숫자로 소프트웨어 품질을 추정하는 유머 사진](http://www.osnews.com/images/comics/wtfm.jpg)

이 글은 소프트웨어 방법론에 관한 책들 중 Robert C. Martin's의 책인 [*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)에 있는 내용을 JavaScript 언어에 적용시켜 적은 글 입니다.
이 글은 단순히 Style Guide가 아니라 JavaScript로 코드를 작성할때 읽기 쉽고, 재사용 가능하며 리팩토링 가능하게끔 작성하도록 도와줍니다.

여기 있는 모든 원칙이 엄격히 지켜져야하는 것은 아니며, 보편적으로 통용되는 원칙은 아닙니다. 이것들은 지침일 뿐이며 `Clean Code`의 저자가 수년간 경험한 내용을 바탕으로 정리한 것입니다.

소프트웨어 엔지니어링 역사는 50년을 조금 넘겼지만 우리는 아직도 많은 것들을 배우고 있습니다.
그리고 소프트웨어 아키텍쳐가 건축설계 만큼이나 오래되었을 때 우리는 아래 규칙들보다 더 엄격한 규칙들을 따라야 할지도 모릅니다.
하지만 지금 당장은 이 가이드 라인을 당신과 당신 팀이 작성하는 JavaScript 코드의 품질을 평가하는 기준으로 삼으세요.

한가지 더 덧붙이자면, 이 원칙들을 알게된다해서 당장 더 나은 개발자가 되는 것은 아니며 코드를 작성할 때 
실수를 하지 않게 해주는 것은 아닙니다. 훌륭한 도자기들이 처음엔 말랑한 점토부터 시작하듯이 모든 코드들은 처음부터 완벽할 수 없습니다.
하지만 당신은 팀원들과 같이 코드를 리뷰하며 점점 완벽하게 만들어가야 합니다. 당신이 처음 작성한 코드를 고칠 때 절대로 자신을 질타하지 마세요.
대신 코드를 부수고 더 나은 코드를 만드세요!


### **함수(Functions)**
### 함수 인자는 2개 이하가 이상적입니다
매개변수의 개수를 제한 하는 것은 함수 테스팅을 쉽게 만들어 주기 때문에 중요합니다. 만약 매개변수가 3개 이상일 경우엔
테스트 해야하는 경우의 수가 많아지고 각기 다른 인수들로 여러 사례들을 테스트 해야합니다.

1개나 2개의 인자를 가지고 있는 것이 가장 이상적인 케이스입니다.
그리고 3개의 인자는 가능한 피해야합니다. 그것보다 더 많다면 통합되어야합니다.
만약 당신이 2개 이상의 인자를 가진 함수를 사용한다면 그 함수에게 너무 많은 역할을 하게 만든 것입니다.
그렇지 않은 경우라면 대부분의 경우 상위 객체는 1개의 인자만으로 충분합니다.

JavaScript를 사용할 때 많은 보일러플레이트 없이 바로 객체를 만들 수 있습니다.
그러므로 당신이 만약 많은 인자들을 사용해야 한다면 객체를 이용할 수 있습니다.

함수가 기대하는 속성을 좀더 명확히 하기 위해서 es6의 비구조화(destructuring) 구문을 사용할 수 있고
이 구문에는 몇가지 장점이 있습니다.

1. 어떤 사람이 그 함수의 시그니쳐(인자의 타입, 반환되는 값의 타입 등)를 볼 때 어떤 속성이 사용되는지
즉시 알 수 있습니다.
2. 또한 비구조화는 함수에 전달된 인수 객체의 지정된 기본타입 값을 복제하며 이는 사이드이펙트가
일어나는 것을 방지합니다. 참고로 인수 객체로부터 비구조화된 객체와 배열은 복제되지 않습니다.
3. Linter를 사용하면 사용하지않는 인자에 대해 경고해주거나 비구조화 없이 코드를 짤 수 없게 할 수 있습니다.



**안좋은 예:**
```javascript
function createMenu(title, body, buttonText, cancellable) {
  // ...
}
```

**좋은 예:**
```javascript
function createMenu({ title, body, buttonText, cancellable }) {
  // ...
}

createMenu({
  title: 'Foo',
  body: 'Bar',
  buttonText: 'Baz',
  cancellable: true
});
```
**[⬆ 상단으로](#목차)**

### 함수는 하나의 행동만 해야합니다
이것은 소프트웨어 엔지니어링에서 가장 중요한 규칙입니다. 함수가 1개 이상의 행동을 한다면 작성하는 것도, 테스트하는 것도, 이해하는 것도 어려워집니다.
당신이 하나의 함수에 하나의 행동을 정의하는 것이 가능해진다면 함수는 좀 더 고치기 쉬워지고 코드들은 읽기 쉬워질 것입니다.
많은 원칙들 중 이것만 알아간다 하더라도 당신은 많은 개발자들을 앞설 수 있습니다.

**안좋은 예:**
```javascript
function emailClients(clients) {
  clients.forEach(client => {
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive()) {
      email(client);
    }
  });
}
```

**좋은 예:**
```javascript
function emailClients(clients) {
  clients
    .filter(isClientActive)
    .forEach(email);
}

function isClientActive(client) {
  const clientRecord = database.lookup(client);
  return clientRecord.isActive();
}
```
**[⬆ 상단으로](#목차)**

### 함수명은 함수가 무엇을 하는지 알 수 있어야 합니다

**안좋은 예:**
```javascript
function AddToDate(date, month) {
  // ...
}

const date = new Date();

// 뭘 추가하는 건지 이름만 보고 알아내기 힘듭니다.
AddToDate(date, 1);
```

**좋은 예:**
```javascript
function AddMonthToDate(date, month) {
  // ...
}

const date = new Date();
AddMonthToDate(date, 1);
```
**[⬆ 상단으로](#목차)**

### 함수는 단일 행동을 추상화 해야합니다
추상화된 이름이 여러 의미를 내포하고 있다면 그 함수는 너무 많은 일을 하게끔 설계된 것입니다.
함수들을 나누어서 재사용가능하고 테스트하기 쉽게 만드세요.

**안좋은 예:**
```javascript
function parseBetterJSAlternative(code) {
  const REGEXES = [
    // ...
  ];

  const statements = code.split(' ');
  const tokens = [];
  REGEXES.forEach(REGEX => {
    statements.forEach(statement => {
      // ...
    });
  });

  const ast = [];
  tokens.forEach(token => {
    // lex...
  });

  ast.forEach(node => {
    // parse...
  });
}
```

**좋은 예:**
```javascript
function tokenize(code) {
  const REGEXES = [
    // ...
  ];

  const statements = code.split(' ');
  const tokens = [];
  REGEXES.forEach(REGEX => {
    statements.forEach(statement => {
      tokens.push( /* ... */ );
    });
  });

  return tokens;
}

function lexer(tokens) {
  const ast = [];
  tokens.forEach(token => {
    ast.push( /* ... */ );
  });

  return ast;
}

function parseBetterJSAlternative(code) {
  const tokens = tokenize(code);
  const ast = lexer(tokens);
  ast.forEach(node => {
    // parse...
  });
}
```
**[⬆ 상단으로](#목차)**

### 중복된 코드를 작성하지 마세요
중복된 코드를 작성하지 않기위해 최선을 다하세요.
중복된 코드가 있다는 것은 어떤 로직을 수정해야 할 일이 생겼을 때 수정 해야할 코드가 한 곳 이상이라는 것을 뜻합니다.

만약 당신이 레스토랑을 운영하면서 토마토나 양파, 마늘, 고추같은 것들의 재고관리를 해야한다고 생각해보세요.
재고가 적혀있는 종이가 여러장 있다면 토마토나 양파의 재고가 변동되었을 때 재고가 적혀있는 모든 종이를 수정해야 합니다.
만약 재고를 관리하는 종이가 한 장이었다면 한 장의 재고 목록만 수정하면 됐겠죠!

종종 코드를 살펴보면 사소한 몇몇의 차이점 때문에 중복된 코드를 작성한 경우가 있고
이런 차이점들은 대부분 똑같은 일을 하는 분리된 함수들을 갖도록 강요합니다.
즉 중복 코드를 제거한다는 것은 하나의 함수 / 모듈 / 클래스를 사용하여 이 여러 가지 사소한 차이점을 처리 할 수 있는
추상화를 만드는 것을 의미합니다.

그리고 추상화 할 부분이 남아있는 것은 위험하기때문에 *클래스* 섹션에 제시된 여러 원칙들을 따라야 합니다.
잘 추상화 하지 못한 코드는 중복된 코드보다 나쁠 수 있으므로 조심하세요. 즉 추상화를 잘 할 수 있다면
그렇게 하라는 말입니다. 코드의 중복을 피한다면 여러분이 원할 때 언제든 한 곳만 수정해도 다른 모든 코드에
반영되게 할 수 있습니다.

**안좋은 예:**
```javascript
function showDeveloperList(developers) {
  developers.forEach(developers => {
    const expectedSalary = developer.calculateExpectedSalary();
    const experience = developer.getExperience();
    const githubLink = developer.getGithubLink();
    const data = {
      expectedSalary,
      experience,
      githubLink
    };

    render(data);
  });
}

function showManagerList(managers) {
  managers.forEach(manager => {
    const expectedSalary = manager.calculateExpectedSalary();
    const experience = manager.getExperience();
    const portfolio = manager.getMBAProjects();
    const data = {
      expectedSalary,
      experience,
      portfolio
    };

    render(data);
  });
}
```

**좋은 예:**
```javascript
function showEmployeeList(employees) {
  employees.forEach((employee) => {
    const expectedSalary = employee.calculateExpectedSalary();
    const experience = employee.getExperience();

    let portfolio = employee.getGithubLink();

    if (employee.type === 'manager') {
      portfolio = employee.getMBAProjects();
    }

    const data = {
      expectedSalary,
      experience,
      portfolio
    };

    render(data);
  });
}
```
**[⬆ 상단으로](#목차)**

### Object.assign을 사용해 기본 객체를 만드세요

**안좋은 예:**
```javascript
const menuConfig = {
  title: null,
  body: 'Bar',
  buttonText: null,
  cancellable: true
};

function createMenu(config) {
  config.title = config.title || 'Foo';
  config.body = config.body || 'Bar';
  config.buttonText = config.buttonText || 'Baz';
  config.cancellable = config.cancellable !== undefined ? config.cancellable : true;
}

createMenu(menuConfig);
```

**좋은 예:**
```javascript
const menuConfig = {
  title: 'Order',
  // 유저가 'body' key의 value를 정하지 않았다.
  buttonText: 'Send',
  cancellable: true
};

function createMenu(config) {
  config = Object.assign({
    title: 'Foo',
    body: 'Bar',
    buttonText: 'Baz',
    cancellable: true
  }, config);

  // config는 이제 다음과 동일합니다: {title: "Order", body: "Bar", buttonText: "Send", cancellable: true}
  // ...
}

createMenu(menuConfig);
```
**[⬆ 상단으로](#목차)**

### 매개변수로 플래그를 사용하지 마세요
플래그를 사용하는 것 자체가 그 함수가 한가지 이상의 역할을 하고 있다는 것을 뜻합니다.
boolean 기반으로 함수가 실행되는 코드가 나뉜다면 함수를 분리하세요.

**안좋은 예:**
```javascript
function createFile(name, temp) {
  if (temp) {
    fs.create(`./temp/${name}`);
  } else {
    fs.create(name);
  }
}
```

**좋은 예:**
```javascript
function createFile(name) {
  fs.create(name);
}

function createTempFile(name) {
  createFile(`./temp/${name}`);
}
```
**[⬆ 상단으로](#목차)**

### 사이드 이펙트를 피하세요 (part 1)
함수는 값을 받아서 어떤 일을 하거나 값을 리턴할 때 사이드 이팩트를 만들어냅니다.
사이드 이팩트는 파일에 쓰여질 수도 있고, 전역 변수를 수정할 수 있으며, 실수로 모든 돈을 다른 사람에게 보낼 수도 있습니다.

당신은 때때로 프로그램에서 사이드 이팩트를 만들어야 할 때가 있습니다. 아까 들었던 예들 중 하나인 파일작성을 할 때와 같이 말이죠.
이 때 여러분이 해야할 일은 파일 작성을 하는 한 개의 함수를 만드는 일 입니다. 파일을 작성하는 함수나 클래스가
여러개 존재하면 안됩니다. 반드시 하나만 있어야 합니다.

즉, 어떠한 구조체도 없이 객체 사이의 상태를 공유하거나, 무엇이든 쓸 수 있는 변경 가능한 데이터 유형을 사용하거나,
같은 사이드 이펙트를 만들어내는 것을 여러개 만들거나하면 안됩니다. 여러분들이 이러한 것들을 지키며 코드를 작성한다면
대부분의 다른 개발자들보다 행복할 수 있습니다.

**안좋은 예:**
```javascript
// 아래 함수에 의해 참조되는 전역 변수입니다.
// 이 전역 변수를 사용하는 또 하나의 함수가 있다고 생각해보세요. 이제 이 변수는 배열이 될 것이고, 프로그램을 망가뜨리겠죠.
let name = 'Ryan McDermott';

function splitIntoFirstAndLastName() {
  name = name.split(' ');
}

splitIntoFirstAndLastName();

console.log(name); // ['Ryan', 'McDermott'];
```

**좋은 예:**
```javascript
function splitIntoFirstAndLastName(name) {
  return name.split(' ');
}

const name = 'Ryan McDermott';
const newName = splitIntoFirstAndLastName(name);

console.log(name); // 'Ryan McDermott';
console.log(newName); // ['Ryan', 'McDermott'];
```
**[⬆ 상단으로](#목차)**

### 사이드 이펙트를 피하세요 (part 2)
자바스크립트에서는 기본타입 자료형은 값을 전달하고 객체와 배열은 참조를 전달합니다.
객체와 배열인 경우를 한번 살펴봅시다. 우리가 만든 함수는 장바구니 배열에 변화를 주며
이 변화는 구매목록에 어떤 상품을 추가하는 기능 같은 것을 말합니다.
만약 `장바구니` 배열을 사용하는 어느 다른 함수가 있다면 이러한 추가에 영향을 받습니다.
이것은 좋을 수도 있지만, 안좋을 수도 있습니다. 안좋은 예를 한번 상상해봅시다.

유저가 구매하기 버튼을 눌러 `구매` 함수를 호출합니다. 이는 네트워크 요청을 생성하고 서버에 `장바구니` 배열을 보냅니다.
하지만 네트워크 연결이 좋지않아서 `구매` 함수는 다시한번 네트워크 요청을 보내야 하는 상황이 생겼습니다.
이때, 사용자가 네트워크 요청이 시작되기 전에 실수로 원하지 않는 상품의 "장바구니에 추가" 버튼을 실수로 클릭하면 어떻게될까요?
실수가 있고난 뒤, 네트워크 요청이 시작되면 `장바구니에 추가` 함수 때문에 실수로 변경된 `장바구니` 배열을 서버에 보내게 됩니다.

가장 좋은 방법은 `장바구니에 추가`는 항상 `장바구니` 배열을 복제하여 수정하고 복제본을 반환하는 것입니다.
이렇게하면 장바구니 참조를 보유하고있는 다른 함수가 다른 변경 사항의 영향을 받지 않게됩니다.

이 접근법에대해 말하고 싶은 것이 두가지 있습니다.

1. 실제로 입력된 객체를 수정하고 싶은 경우가 있을 수 있지만 이러한 예제를 생각해보고 적용해보면 그런 경우는
거의 없다는 것을 깨달을 수 있습니다. 그리고 대부분의 것들이 사이드 이펙트 없이 리팩토링 될 수 있습니다.
2. 큰 객체를 복제하는 것은 성능 측면에서 값이 매우 비쌉니다. 운좋게도 이런게 큰 문제가 되지는 않습니다.
왜냐하면 이러한 프로그래밍 접근법을 가능하게해줄 [좋은 라이브러리](https://facebook.github.io/immutable-js/)가 있기 때문입니다.
이는 객체와 배열을 수동으로 복제하는 것처럼 메모리 집약적이지 않게 해주고 빠르게 복제해줍니다.

**Bad:**
```javascript
const addItemToCart = (cart, item) => {
  cart.push({ item, date: Date.now() });
};
```

**Good:**
```javascript
const addItemToCart = (cart, item) => {
  return [...cart, { item, date : Date.now() }];
};
```
**[⬆ 상단으로](#목차)**

### 전역 함수를 사용하지 마세요
전역 환경을 사용하는 것은 JavaScript에서 나쁜 관행입니다. 왜냐하면 다른 라이브러리들과의 충돌이 일어날 수 있고,
당신의 API를 쓰는 유저들은 운영환경에서 예외가 발생하기 전까지는 문제를 인지하지 못할 것이기 때문입니다. 예제를 하나 생각해봅시다.
JavaScript의 네이티브 Array 메소드를 확장하여 두 배열 간의 차이를 보여줄 수있는 `diff` 메소드를 사용하려면 어떻게 해야할까요? 
새로운 함수를 `Array.prototype`에 쓸 수도 있지만, 똑같은 일을 시도한 다른 라이브러리와 충돌 할 수 있습니다.
다른 라이브러리가 `diff` 메소드를 사용하여 첫번째 요소와 마지막 요소의 차이점을 찾으면 어떻게 될까요?
이것이 그냥 ES2015/ES6의 classes를 사용해서 전역 `Array`를 상속해버리는 것이 훨씬 더 나은 이유입니다.

**안좋은 예:**
```javascript
Array.prototype.diff = function diff(comparisonArray) {
  const hash = new Set(comparisonArray);
  return this.filter(elem => !hash.has(elem));
};
```

**좋은 예:**
```javascript
class SuperArray extends Array {
  diff(comparisonArray) {
    const hash = new Set(comparisonArray);
    return this.filter(elem => !hash.has(elem));
  }
}
```
**[⬆ 상단으로](#목차)**

### 명령형 프로그래밍보다 함수형 프로그래밍을 지향하세요
JavaScript는 Haskell처럼 함수형 프로그래밍 언어는 아니지만 함수형 프로그래밍처럼 작성할 수 있습니다.
함수형 언어는 더 깔끔하고 테스트하기 쉽습니다. 가능하면 이 방식을 사용하도록 해보세요.

**안좋은 예:**
```javascript
const programmerOutput = [
  {
    name: 'Uncle Bobby',
    linesOfCode: 500
  }, {
    name: 'Suzie Q',
    linesOfCode: 1500
  }, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
  }, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
  }
];

let totalOutput = 0;

for (let i = 0; i < programmerOutput.length; i++) {
  totalOutput += programmerOutput[i].linesOfCode;
}
```

**좋은 예:**
```javascript
const programmerOutput = [
  {
    name: 'Uncle Bobby',
    linesOfCode: 500
  }, {
    name: 'Suzie Q',
    linesOfCode: 1500
  }, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
  }, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
  }
];

const totalOutput = programmerOutput
  .map(programmer => programmer.linesOfCode)
  .reduce((acc, linesOfCode) => acc + linesOfCode, INITIAL_VALUE);
```
**[⬆ 상단으로](#목차)**

### 조건문을 캡슐화 하세요

**안좋은 예:**
```javascript
if (fsm.state === 'fetching' && isEmpty(listNode)) {
  // ...
}
```

**좋은 예:**
```javascript
function shouldShowSpinner(fsm, listNode) {
  return fsm.state === 'fetching' && isEmpty(listNode);
}

if (shouldShowSpinner(fsmInstance, listNodeInstance)) {
  // ...
}
```
**[⬆ 상단으로](#목차)**

### 부정조건문을 사용하지 마세요

**안좋은 예:**
```javascript
function isDOMNodeNotPresent(node) {
  // ...
}

if (!isDOMNodeNotPresent(node)) {
  // ...
}
```

**좋은 예:**
```javascript
function isDOMNodePresent(node) {
  // ...
}

if (isDOMNodePresent(node)) {
  // ...
}
```
**[⬆ 상단으로](#목차)**

### 조건문 작성을 피하세요
조건문 작성을 피하라는 것은 매우 불가능한 일로 보입니다. 이 얘기를 처음 듣는 사람들은 대부분 "`If`문 없이 어떻게 코드를 짜나요?"라고 말합니다.
하지만 다형성을 이용한다면 동일한 작업을 수행할 수 있습니다. 두번째 질문은 보통 "네 좋네요 근데 내가 왜 그렇게 해야하나요?"이죠.
그에 대한 대답은, 앞서 우리가 공부했던 clean code 컨셉에 있습니다. 함수는 단 하나의 일만 수행하여야 합니다.
당신이 함수나 클래스에 `if`문을 쓴다면 그것은 그 함수나 클래스가 한가지 이상의 일을 수행하고 있다고 말하는 것과 같습니다.
기억하세요, 하나의 함수는 딱 하나의 일만 해야합니다.

**안좋은 예:**
```javascript
class Airplane {
  // ...
  getCruisingAltitude() {
    switch (this.type) {
      case '777':
        return this.getMaxAltitude() - this.getPassengerCount();
      case 'Air Force One':
        return this.getMaxAltitude();
      case 'Cessna':
        return this.getMaxAltitude() - this.getFuelExpenditure();
    }
  }
}
```

**좋은 예:**
```javascript
class Airplane {
  // ...
}

class Boeing777 extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude() - this.getPassengerCount();
  }
}

class AirForceOne extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude();
  }
}

class Cessna extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude() - this.getFuelExpenditure();
  }
}
```
**[⬆ 상단으로](#목차)**

### 타입-체킹을 피하세요 (part 1)
JavaScript는 타입이 정해져있지 않습니다. 이는 당신의 함수가 어떤 타입의 인자든 받을 수 있다는 것을 의미합니다.
이런 JavaScript의 자유로움 때문에 여러 버그가 발생했었고 이 때문에 당신의 함수에 타입-체킹을 시도 할 수도 있습니다.
하지만 타입-체킹 말고도 이러한 화를 피할 많은 방법들이 존재합니다. 첫번째 방법은 일관성 있는 API를 사용하는 것입니다.

**안좋은 예:**
```javascript
function travelToTexas(vehicle) {
  if (vehicle instanceof Bicycle) {
    vehicle.pedal(this.currentLocation, new Location('texas'));
  } else if (vehicle instanceof Car) {
    vehicle.drive(this.currentLocation, new Location('texas'));
  }
}
```

**좋은 예:**
```javascript
function travelToTexas(vehicle) {
  vehicle.move(this.currentLocation, new Location('texas'));
}
```
**[⬆ 상단으로](#목차)**

### 타입-체킹을 피하세요 (part 2)
당신이 문자열, 정수, 배열등 기본 자료형을 사용하고 다형성을 사용할 수 없을 때 여전히 타입-체킹이 필요하다고 느껴진다면
TypeScript를 도입하는 것을 고려해보는 것이 좋습니다. TypeScript는 표준 JavaScript 구문에 정적 타입을 제공하므로
일반 JavaScript의 대안으로 사용하기에 좋습니다. JavaScript에서 타입-체킹을 할 때 문제점은 가짜 `type-safety`
를 얻기위해 작성된 코드를 설명하기 위해서 많은 주석을 달아야한다는 점입니다. JavaScript로 코드를 작성할땐 깔끔하게 코드를 작성하고,
좋은 테스트 코드를 짜야하며 좋은 코드 리뷰를 해야합니다. 그러기 싫다면 그냥 TypeScript(이건 제가 말했듯이, 좋은 대체재입니다!)를 쓰세요.

**안좋은 예:**
```javascript
function combine(val1, val2) {
  if (typeof val1 === 'number' && typeof val2 === 'number' ||
      typeof val1 === 'string' && typeof val2 === 'string') {
    return val1 + val2;
  }
  
  throw new Error('Must be of type String or Number');
}
```

**좋은 예:**
```javascript
function combine(val1, val2) {
  return val1 + val2;
}
```
**[⬆ 상단으로](#목차)**

### 과도한 최적화를 지양하세요
최신 브라우저들은 런타임에 많은 최적화 작업을 수행합니다. 대부분 당신이 코드를 최적화 하는 것은 시간낭비일 가능성이 많습니다.
최적화가 부족한 곳이 어딘지를 알려주는 [좋은 자료](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)가 여기 있습니다.
이것을 참조하여 최신 브라우저들이 최적화 해주지 않는 부분만 최적화를 해주는 것이 좋습니다.

**안좋은 예:**
```javascript

// 오래된 브라우저의 경우 캐시되지 않은 `list.length`를 통한 반복문은 높은 코스트를 가졌습니다.
// 그 이유는 `list.length`를 매번 계산해야만 했기 때문인데, 최신 브라우저에서는 이것이 최적화 되었습니다.
for (let i = 0, len = list.length; i < len; i++) {
  // ...
}
```

**좋은 예:**
```javascript
for (let i = 0; i < list.length; i++) {
  // ...
}
```
**[⬆ 상단으로](#목차)**

### 죽은 코드를 지우세요

죽은 코드는 중복된 코드 만큼이나 좋지 않습니다. 죽은 코드는 당신의 코드에 남아있을 어떠한 이유도 없습니다.
호출되지 않는 코드가 있다면 그 코드는 지우세요! 그 코드가 여전히 필요해도 그 코드는 버전 히스토리에 안전하게
남아있을 것입니다. -> **linter 사용하면 IDE 에서 안쓰는 코드를 알 수 있다.** 

**안좋은 예:**
```javascript
function oldRequestModule(url) {
  // ...
}

function newRequestModule(url) {
  // ...
}

const req = newRequestModule;
inventoryTracker('apples', req, 'www.inventory-awesome.io');

```

**좋은 예:**
```javascript
function newRequestModule(url) {
  // ...
}

const req = newRequestModule;
inventoryTracker('apples', req, 'www.inventory-awesome.io');
```
**[⬆ 상단으로](#목차)**

----
## ○ 참조 문서 및 사이트
* [clean-code-javascript-ko](https://github.com/qkraudghgh/clean-code-javascript-ko)
