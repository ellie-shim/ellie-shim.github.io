---
layout: post
title: "5주차- REACT - 1 - JSX"
subtitle: "siots"
categories: siots
tags: topic
comments: true
---

# 5주차 topic -

# JSX

- 리액트에서 사용할 수 있는 자바스크립트의 확장문법입니다.

- JSX도 표현식이기 때문에 `if`문이나 `for`문 안에서 JSX를 사용할 수 있으며, 변수에 할당하거나 매개변수로 전달하거나 함수에서 반환할 수 있습니다.

- HTML 어트리뷰트를 넘길 때 `camelCase`를 사용합니다. 어트리뷰트의 이름 그대로를 사용하지 않는 경우도 있습니다 (`class` => `className`, label의 `for` => `htmlFor`)

- 여는 태그만 있다면 `/>`를 이용해 닫아주어야 합니다.

- JSX를 사용할 때에는 코드의 스코프 안에 React 라이브러리가 항상 존재해야합니다.

- 점 표기법을 사용할 수 있습니다.

  - 하나의 모듈에서 여러 React 컴포넌트를 export 하는 경우에 편리하게 쓸 수 있습니다.

  - `MyComponents.DatePicker`가 컴포넌트라면 아래와 같이 사용할 수 있습니다.

  ```js
  import React from "react";

  const MyComponents = {
    DatePicker: function DatePicker(props) {
      return <div>Imagine a {props.color} datepicker here.</div>;
    }
  };

  function BlueDatePicker() {
    return <MyComponents.DatePicker color="blue" />;
  }
  ```

- 사용자 정의 컴포넌트는 대문자로 시작해야합니다.
  - 엘리먼트 타입이 소문자로 시작한다는것은 그것이 내장 컴포넌트(`<div>`, `<span>`과 같은)라는 것을 뜻합니다.

## JSX 안에서 prop 사용하기

#### 1. JavaScript 표현식

`{}`로 둘러싼 JavaScript 표현식을 prop으로 사용할 수 있습니다.

`{}`안의 표현식의 계산된 값이 prop이 됩니다.

`if`와 `for`구문은 표현식이 아니기때문에 JSX안에서 그대로 사용할 수는 없고 아래와 같이 사용 가능합니다.

```js
function NumberDescriber(props) {
  let description;
  if (props.number % 2 == 0) {
    description = <strong>even</strong>;
  } else {
    description = <i>odd</i>;
  }
  return (
    <div>
      {props.number} is an {description} number
    </div>
  );
}
```

#### 2. 문자열 리터럴

아래 두 JSX 표현식은 동일하게 동작합니다.

```js
<MyComponent message="hello world" />

<MyComponent message={'hello world'} />
```

#### 3. Props의 기본값은 true 입니다.

```js
<MyTextBox autocomplete />
<MyTextBox autocomplete={true} />
```

prop으로 아무값도 넘겨주지않으면 기본값인 `true`가 됩니다.
하지만 이 방법을 권장하지는 않습니다.

#### 4. 속성 펼치기

props로 넘겨줄 객체를 가지고 있다면 `...`(spread 연산자)을 사용하여 객체 전체를 쉽게 넘겨줄 수 있습니다.

아래 두 코드는 동일하게 동작합니다.

```js
function App1() {
  return <Greeting firstName="Ben" lastName="Hector" />;
}

function App2() {
  const props = { firstName: "Ben", lastName: "Hector" };
  return <Greeting {...props} />;
}
```

특정 prop을 골라내고 나머지 prop을 다른 컴포넌트에 넘겨줄때에서 사용할 수 있습니다.

```js
const Button = props => {
  const { kind, ...other } = props;
  const className = kind === "primary" ? "PrimaryButton" : "SecondaryButton";
  return <button className={className} {...other} />;
};

const App = () => {
  return (
    <div>
      <Button kind="primary" onClick={() => console.log("clicked!")}>
        Hello World!
      </Button>
    </div>
  );
};
```

![props가 넘겨진것 확인](https://ellie-shim.github.io/assets/img/topic-5-jsx.PNG)
위 예제에서는 `kind` prop이 안전하게 추출되었고 DOM의 `<button>`요소로는 전달되지 않았습니다. 다른 모든 prop들은 `...other` 객체를 통해 전달되었고, 이 방법을 통해 컴포넌트를 굉장히 유연하게 만들 수 있습니다. `onClick`과 `children` prop가 넘겨진 모습을 확인해보세요.

속성 펼치기 기법은 유용하게 사용될 수 있지만 **불필요한 props 혹은 틀린 어트리뷰트를 컴포넌트에 넘기게 되는 일이 생기기 쉽다**는 단점도 있습니다.

## JSX에서 자식 다루기

#### 1. 문자열 리터럴

여는 태그와 닫는 태그 사이에 있는 문자열은 `props.children`이 됩니다.

1. 각 줄의 처음과 끝에 있는 공백을 제거합니다.
1. 빈 줄이 삭제됩니다.
1. 태그에 붙어있는 개행이 삭제됩니다.
1. 문자열 리터럴 중간에 등장하는 여거래의 개행은 한개의 공백으로 줄어듭니다.

기본적으로, React에서는 cross-site-scripting(XSS) 공격을 막기 위하여 렌더링 되기 전에 JSX 내에 포함된 모든 값을 이스케이프 합니다. 따라서 모든 것은 렌더링 되기 전에 문자열로 변환됩니다.

`props.children`에서는 HTML 이스케이핑이 풀리게 되므로, 보통의 HTML을 사용할 수 있습니다.

![jsx의 이스케이프](https://ellie-shim.github.io/assets/img/topic-5-jsx2.PNG)

[Tip. JSX의 XSS 방어를 무시하고 html코드를 출력하고 싶을 때 ](https://velopert.com/1896)

> 문자의 이스케이프

```
& becomes &amp;
< becomes &lt;
> becomes &gt;
" becomes &quot;
' becomes &#39;
```

#### 2. JSX를 자식으로 사용하기

JSX 엘리먼트를 자식으로 넘겨줄 수도 있습니다. 이는 중첩된 컴포넌트를 보여주고 싶을 때 유리합니다.

```js
<MyContainer>
  <MyFirstComponent />
  <MySecondComponent />
</MyContainer>
```

엘리먼트로 이루어진 배열 역시 반환할 수 있습니다.

```js
render() {
  // 별도의 엘리먼트로 감싸줄 필요가 없습니다!
  return [
    // 키를 잊지 마세요 :)
    <li key="A">First item</li>,
    <li key="B">Second item</li>,
    <li key="C">Third item</li>,
  ];
}
```

위 코드는 아래처럼 그려집니다.

![엘리먼트로 이루어진 배열](https://ellie-shim.github.io/assets/img/topic-5-jsx3.PNG)

#### 3. JavaScript 표현식을 자식으로 사용하기

`{}`로 둘러싼 JavaScript 표현식은 모두 자식이 될 수 있습니다.
배열을 렌더링하고 싶을 때 자주 사용됩니다.

```js
function Item(props) {
  return <li>count {props.count}</li>;
}

function TodoList() {
  const todos = ["finish doc", "submit pr", "nag dan to review"];
  return (
    <ul>
      {todos.map(message => (
        <Item key={message} message={message} />
      ))}
    </ul>
  );
}
```

#### 3. 함수를 자식으로 사용하기

`props.children`은 다른 prop들과 같은 방식으로 동작하며 어떤 형태의 데이터도 넘겨질 수 있습니다.

아래 소스처럼 `props.children`에 함수를 넘겨줄 수도 있습니다.

```js
function Repeat(props) {
  let items = [];
  for (let i = 0; i < props.numTimes; i++) {
    items.push(props.children(i));
  }
  return <div>{items}</div>;
}
class App extends React.Component {
  render() {
    return (
      <Repeat numTimes={10}>
        {index => <div key={index}>This is item {index} in the list</div>}
      </Repeat>
    );
  }
}
```

![함수를 자식으로 사용하기](https://ellie-shim.github.io/assets/img/topic-5-jsx4.PNG)

1. `Repeat`의 props.children에는 `(index) => <div key={index}>This is item {index} in the list</div>` 라는 함수가 들어갑니다.

1. props.children에 함수가 들어갔기 때문에 `items.push(props.children(i));` 이런식으로 사용할 수 있습니다.

> 이거 무슨 말인지 모르겠어용,,

#### 4. 진리값, null, undefined는 무시됩니다.

`false`, `null`, `undefined`, `true` 는 유효한 자식입니다. 하지만 화면에 아무것도 그려지지 않습니다. 아래 JSX 표현식은 모두 같은 결과를 렌더링합니다

```js
<div />

<div></div>

<div>{false}</div>

<div>{null}</div>

<div>{undefined}</div>

<div>{true}</div>
```

하지만 모든 `falsy`값이 해당되는 것은 아닙니다. `0`과 `NaN`은 `false`로 처리되지않고 화면에 그려집니다.

`false`, `true`, `null`, `undefined` 를 출력시키고 싶다면, 먼저 문자열로 변환 해야합니다.

```js
<div>My JavaScript variable is {String(myVariable)}.</div>
```

# JSX를 사용하지 않는 React

React를 할 때 JSX는 필수사항이 아닙니다.
JSX는 `React.createElement(component, props, ...children)`을 호출하는 문법 설탕입니다. 그래서 JSX에서 할 수 있는 모든 일은 순수 자바스크립트에서도 할 수 있습니다.

JSX를 사용한 코드

```js
class Hello extends React.Component {
  render() {
    return <div>Hello {this.props.toWhat}</div>;
  }
}

ReactDOM.render(<Hello toWhat="World" />, document.getElementById("root"));
```

순수 자바스크립트 코드

```js
class Hello extends React.Component {
  render() {
    return React.createElement("div", null, `Hello ${this.props.toWhat}`);
  }
}

ReactDOM.render(
  React.createElement(Hello, { toWhat: "World" }, null),
  document.getElementById("root")
);
```

`React.createElement`를 변수에 할당해 더 편하게 작업할 수 있습니다.

```js
const e = React.createElement;

ReactDOM.render(e("div", null, "Hello World"), document.getElementById("root"));
```

---

[온라인 바벨 컴파일러](https://babeljs.io/repl/#?presets=react&code_lz=GYVwdgxgLglg9mABACwKYBt1wBQEpEDeAUIogE6pQhlIA8AJjAG4B8AEhlogO5xnr0AhLQD0jVgG4iAXyJA)에 아래 코드를 넣어보고 어떻게 컴파일 되는지 확인해보세용

```js
class Hello extends React.Component {
  render() {
    return (
      <div>
        <h1>hello</h1>
        {this.props.name}
      </div>
    );
  }
}
ReactDOM.render(<Hello name="Ellie" />, document.getElementById("root"));
```

# ES6를 사용하지 않는 React

#### 클래스

보통 React 컴포넌트는 순수 자바스크립트 클래스로 정의합니다.

아직 ES6를 사용하지 않는다면 클래스 대신 `create-react-class`를 사용할 수 있습니다. ES6의 클래스와 일부 제외하고 비슷하게 동작합니다.

ES6 클래스를 사용한 코드

```js
class Greeting extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

ES6를 사용하지 않은 코드

```js
var createReactClass = require("create-react-class");
var Greeting = createReactClass({
  render: function() {
    return <h1>Hello, {this.props.name}</h1>;
  }
});
```

#### Props 기본값 선언

ES6 클래스로 만든 컴포넌트에는 `defaultProps` 속성을 정의할 수 있습니다.
`createReactClass()` 를 이용할 때는 객체에 함수를 전달하기 위해 `getDefaultProps()` 를 정의해주어야 합니다.

ES6 사용한 코드

```js
class Greeting extends React.Component {
  // ...
}

Greeting.defaultProps = {
  name: "Mary"
};
```

ES6를 사용하지 않은 코드

```js
var Greeting = createReactClass({
  getDefaultProps: function() {
    return {
      name: "Mary"
    };
  }

  // ...
});
```

#### 초기 state 설정

`createReactClass()` 를 이용할 때는 기초 state를 반환하는 개별 `getInitialState` 메소드를 사용합니다.

ES6 사용한 코드

```js
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: props.initialCount };
  }
  // ...
}
```

ES6를 사용하지 않은 코드

```js
var Counter = createReactClass({
  getInitialState: function() {
    return { count: this.props.initialCount };
  }
  // ...
});
```

#### Autobinding

1. ES6로 선언한 React 컴포넌트에서 메소드는 `this`를 바인딩해주어야합니다.

2. `createReactClass()` 에서는 모든 메서드를 바인드하기 때문에 따로 바인딩 작업을 하지 않습니다.

```js
// 1.
this.handleClick = this.handleClick.bind(this);
```

메소드를 선언할 때 화살표 함수를 이용해서 선언해주어도 바인딩되지만 이는 **실험 기능**이며 언어에서 명확히 제안되지 않았습니다.

```js
handleClick = () => {
  alert(this.state.message);
};
```

확실하게 `this`를 바인딩 하는 방법은

- 생성자(constructor)에서 bind 메소드 사용하기 (1번)
- `createReactClass()` 사용하기 (2번)
- arrow함수 사용하기 `onClick={(e) => this.handleClick(e)}`
