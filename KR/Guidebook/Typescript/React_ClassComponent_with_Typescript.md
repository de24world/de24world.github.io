****
# React Class Component with Typescript

## 1. public 을 class 안에 작성하지 마라 
***
### Don't:
```typescript
class App extends Component {
  public handleChange() {}
  public render() {
      return <div>Hello</div>
  }
}
```
### Do:
```typescript
 class App extends Component {
  handleChange() {}
  render() {
      return <div>Hello</div>
  }
}
```
### Why?
class 내의 모든 멤버는 기본적으로 `public` 입니다. (그리고 항상 runtime에 있는 public도, TS private/protected 만 특별히 class properties(속성들)/methods 만 오직 컴파일 하는 시간 동안만 숨겨집니다) 코드 베이스 추가 이탈을 만들지 마세요. 그리고 publicaccessor(공용 접근권한?)이 유효하고/관용적인 javascript가 아닙니다.

## 2. `private` 접근권한자(accessor) 를 class 컴퍼넌트 안에 작성하지 마세요.
***
### Don't:
```typescript
class App extends Component {
  private handleChange = (ev: import('react).ChangeEvent) => {}
  render() {
      return (
          <div>
            <input onChange={this.handleChange} />
          </div>
      )
  }
}
```
### Good:
```typescript
class App extends Component {
  _private _handleChange = (ev: import('react).ChangeEvent) => {}
  render() {
      return (
          <div>
            <input onChange={this.handleChange} />
          </div>
      )
  }
}
```
### Why?
private 접근자는 런타임하는동안 properties/methods를 class를 private 하게 만들어주지 않습니다. 그것은 단지 타입스크립트 "컴파일하는동안만 에뮬레이션일 뿐입니다. 만약 "private" 하게 만들어주고 싶다면 아래의 패턴을 사용하세요.
* `_someProp` 처럼 이름 앞에 underscore(밑줄)로 시작하세요
* 굳이 proterties를 private 하게 만들고 싶다면 [Symbol](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Symbol) 문법을 사용하세요.

실질적으로는 React Component 인스턴스를 accessing 할 필요가 거의 없습니다.

## 3. Component class에 `protected` 접근권한자(accessor) 를 사용하지 마세요
***
### Don't:
```typescript
class App extends Component {
  private handleChange = (ev: import('react).ChangeEvent) => {}
  render() {
      return (
          <div>
            <input onChange={this.handleChange} />
          </div>
      )
  }
}
```
### Good:
```typescript
class App extends Component {
  _private _handleChange = (ev: import('react).ChangeEvent) => {}
  render() {
      return (
          <div>
            <input onChange={this.handleChange} />
          </div>
      )
  }
}
```
### Why?
private 접근자는 런타임하는동안 properties/methods를 class를 private 하게 만들어주지 않습니다. 그것은 단지 타입스크립트 "컴파일하는동안만 에뮬레이션일 뿐입니다. 만약 "private" 하게 만들어주고 싶다면 아래의 패턴을 사용하세요.
* `_someProp` 처럼 이름 앞에 underscore(밑줄)로 시작하세요
* 굳이 proterties를 private 하게 만들고 싶다면 [Symbol](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Symbol) 문법을 사용하세요.

실질적으로는 React Component 인스턴스를 accessing 할 필요가 거의 없습니다.




## ○ 참고문서
* [10++ TypeScript Pro tips/patterns with (or without) React](https://medium.com/@martin_hotell/10-typescript-pro-tips-patterns-with-or-without-react-5799488d6680#78b9)
****
