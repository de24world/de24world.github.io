[Jest]] Jest
======================
# 1. Enzyme? 
* Enzyme은 airbnb에서 개발한 React용 컴포넌트 테스트 플러그인입니다. 컴포넌트를 얖게(shallow) 렌더링해서 테스트 해 볼 수 있고, 전체 DOM을 불러와 이벤트를 시물레이트 할 수도 있고(ex. 버튼클릭, 인풋 수정, 폼 등록 등) 모든 라이프 사이클이 문제 없이 돌아가는지도 확인할 수 있습니다.

## 1.0 Enzyme?, Jest?, React Testing Library?
* `Jest`는 테스트 Framework이며, `Enzyme`은 라이브러리로 Jest가 좀 더 큰 개념이다.   
`Enzyme`은 Implementation Driven Test(구현 주도 테스트) 방법론을 따르는 테스트를 작성하기에 용이한 테스트 라이브러리로써, 가상 DOM 기준으로 테스트를 작성해야하며 props나 state 검증하기에 용이합니다. `React Testing Library`는 Behavior Driven Test 방밥론을 따르는 테스트를 작성하는데 적합하며 사용자 브라우저에서 랜더링하는 실제 HTML 마크업의 모습이 어떤지에 대해서 테스트하기 용이합니다. 만약 React 를 함수형 컴포넌트로 작성한다며, Enzyme 함수형 컴포넌트를 제한적으로 지원하기 때문에 React Testing Library 추천한다.

## 1.1 설치
```
$ yarn add enzyme enzyme-adapter-react-16
# 또는 npm install --save enzyme enzyme-adapter-react-16
```

## 1.2 핵심 기능 (Core features)
* shallow: 간단한 컴포넌트를 메모리에 렌더링합니다. ( 단일 컴포넌트를 테스트할 때 유용합니다. )
* mount: HOC나 자식 컴포넌트 까지 전부 렌더링합니다. ( 다른 컴포넌트와의 관계를 테스트할 때 유용합니다. )
* render: 컴포넌트를 정적인 html로 렌더링합니다. ( 컴포넌트가 브라우저에 붙었을 때 html로 어떻게 되는지 판단할 때 사용합니다.)

** 라이프사이클 훅 호출 여부는 `mount` API와 `shallow` API가 상이하므로 유의가 필요하다. 간단하게 정리하면 `mount` API는 모든 라이프사이클 훅이 호출되고 `shallow` API는 `componentDidMount`와 `componentDidUpdate`를 제외하고 라이프사이클 훅이 호출된다. 이러한 차이점에 유의하여 선별적으로 API를 사용하도록 하자.

## 1.3 사용 예시
* counter.jsx
```javscript
import React, { Component } from 'react';

export default class Counter extends Component {
  state = {
    value: 0,
    title: '',
  }

  changeTitle = (e) => {
    this.setState(() => ({ title: e.target.value }));
  }

  increment = () => {
    this.setState(prevState => ({ value: prevState.value + 1 }));
  };

  render() {
    return (
      <div>
        <input value={this.state.title} id="title" onChange={this.changeTitle} />
        <b>{this.state.value}</b>
        <button id="up" onClick={this.increment}>증가</button>
      </div>
    );
  }
}
```

* counter-test.jsx
```javascript
import React from 'react';
import Counter from './counter.jsx';
import { shallow, configure } from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';
configure({ adapter: new Adapter() });

describe('<Counter />', () => {
  it('성공적으로 렌더링되어야 합니다.', () => {
    const wrapper = shallow(<Counter />);
    expect(wrapper.length).toBe(1);
  });

  it('타이틀 인풋이 렌더링되어야 합니다.', () => {
    const wrapper = shallow(<Counter />);
    expect(wrapper.find('#title').length).toEqual(1);
  });

  it('타이틀이 변경되어야 합니다.', () => {
    const wrapper = shallow(<Counter />);
    wrapper.find('#title').simulate('change', { target: { value: '값' } });
    expect(wrapper.state().title).toBe('값');
  });

  it('숫자가 올라가야 합니다.', () => {
    const wrapper = shallow(<Counter />);
    wrapper.find('#up').simulate('click');
    wrapper.find('#up').simulate('click');
    expect(wrapper.state().value).toBeLessThan(1);
  });
});
```

## 2.2 목 함수(Mock Functions)

## ○ 참고 영상
* [Jest 강좌 #5 목 함수(Mock Functions) - 자바스크립트 테스트 프레임워크](https://youtu.be/9xBjErtlr1o)
* [빌드(Build)를 위한 Jenkins 설치 및 설정하기](https://youtu.be/m0tky1jyP-0)


## ○ 참조 문서 및 사이트
* [유닛테스트(snap, enzyme)](https://velog.io/@aerirang647/%EC%9C%A0%EB%8B%9B%ED%85%8C%EC%8A%A4%ED%8A%B8#enzyme%EC%9D%84-%ED%86%B5%ED%95%9C-dom-%EC%8B%9C%EB%AE%AC%EB%A0%88%EC%9D%B4%EC%85%98) 
* [Test Utility - Enzyme](https://shs400.github.io/2019/01/23/enzyme/)
* [React 테스트(test, jest, enzyme)](https://www.zerocho.com/category/React/post/583231469a87ec001834a0ec)

