---
layout: single
title: "checked & defaultChecked"
categories: React
tag: [checked, react, 리액트, defaultChecked, radio, input, 라디오, checkbox]
toc: true # table of content 콘텐츠 목록
author_profile: false
sidebar:
  nav: "docs"
---

**[공지사항]** [푸샤 깃허브 블로그 업데이트 사항](https://github.com/de24world/de24world.github.io)
{: .notice--info}

# checked & defaultChecked

기본 엘리먼트에서는 `checked` 속성으로 사용하지만 react 에서는 `defaultChecked`값이 추가되었습니다.
이 두 가지 속성은 역할은 같지만 작은 차이가 있습니다.

```javascript
// radio
<input
	type="radio"
	name="name"
	id="id"
	value="value"
	label="label"
	defaultChecked={true}/>

    // checkbox
<input
	type="checkbox"
	name="name"
	id="id"
	value="value"
	label="label"
	defaultChecked={true}/>
```

## checked

`checked`값을 사용하면 `onChange`값과 함께 사용하여 컨트롤할 수 있습니다.
만약 `onChange` 값이 없으면 해당 컴포넌트는 `readOnly`로 바뀌어 체크를 변경할 수 없습니다.

```js
<input
	type="checkbox"
	name="foo"
	value="bar"
	onChange={(e) => this.setState({ foo: !this.state.foo })}
	checked={this.state.foo}/>

<p>checked: {this.state.foo ? 'true' : 'false'}</p>
```

## defaultChecked

`onChange`값과 관계없이 checked 값을 변경할 수 있습니다.
폼을 `state`로 관리하지 않는다면 `defaultChecked` 값을 사용하는것을 권장합니다.

## checked vs defaultChecked

두개의 값은 같은 성격을 가지고 있기 때문에 한번에 사용할 수 없습니다.
두개의 값이 다 있거나 없으면 `defaultChecked` 값이 우선적으로 사용됨을 주의해주세요.

<div class="notice--success">
<h2>요약</h2>
<ul>
  <li> 만약 onChange 사용하면 checked를 권장하고, state를 onChange로 관리하지않으면 defaultChecked 사용해본다 </li>
  <li> radio나 check 사용시 에러가 뜬다면 현재 사용하고 있는 값을 checked 혹은 defaultChecked를 변경해보자. 필자의 경우 onChange 변경 값(체크 적용)이 제대로 먹히지 않아 한참 디버깅하다가 defaultChecked를 Checked로 변경하니 간단하게 문제해결되었다. (하단 이미지 참조)</li>
</ul>
</div>

<img src="/assets/images/React/checked.png" />

#### 참조 문서 및 사이트

- [참조](https://ui-kit.bbuzzart.com/form/check)

[상단으로](#svg-란){: .btn .btn--primary}
[푸샤 깃허브 이동](https://github.com/de24world){: .btn .btn--info}
