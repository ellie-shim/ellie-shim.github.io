---
layout: post
title: "5주차- REACT "
subtitle: "siots"
categories: siots
tags: topic
comments: true
---

# 5주차 topic - 

# JSX 더 알아보기

리액트에서 사용할 수 있는 자바스크립트의 확장문법입니다.

JSX도 표현식이기 때문에 `if`문이나 `for`문 안에서 JSX를 사용할 수 있으며, 변수에 할당하거나 매개변수로 전달하거나 함수에서 반환할 수 있습니다.

## 리액트 엘리먼트의 타입 지정하기

#### 1. React가 스코프 안에 있어야 합니다.

JSX를 사용할 때에는 코드의 스코프 안에 React 라이브러리가 항상 존재해야합니다.

#### 2. JSX 타입을 위한 점 표기법 사용하기

점 표기법을 사용할 수 있습니다.

하나의 모듈에서 여러 React 컴포넌트를 export 하는 경우에 편리하게 쓸 수 있습니다.

`MyComponents.DatePicker`가 컴포넌트라면 아래와 같이 사용할 수 있습니다.

```js
import React from 'react';

const MyComponents = {
  DatePicker: function DatePicker(props) {
    return <div>Imagine a {props.color} datepicker here.</div>;
  }
}

function BlueDatePicker() {
  return <MyComponents.DatePicker color="blue" />;
}
```

#### 3. 사용자 정의 컴포넌트는 대문자로 시작해야합니다.

엘리먼트 타입이 소문자로 시작한다는것은 그것이 내장 컴포넌트(`<div>`, `<span>`과 같은)라는 것을 뜻합니다.

컴포넌트 이름이 소문자로 시작한다면 우리가 기대한대로 동작하지 않습니다.




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
  return <div>{props.number} is an {description} number</div>;
}
```

#### 2. 문자열 리터럴

아래 두 JSX 표현식은 동일하게 동작합니다.

```js
<MyComponent message="hello world" />

<MyComponent message={'hello world'} />
```

#### 3. Props의 기본값은 true 입니다.

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
  const props = {firstName: 'Ben', lastName: 'Hector'};
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
![props가 넘겨진것 확인](https://bbgrams.github.io/assets/img/topic-5-jsx.png)
위 예제에서는 `kind` prop이 안전하게 추출되었고 DOM의 `<button> `요소로는 전달되지 않았습니다. 다른 모든 prop들은 `...other` 객체를 통해 전달되었고, 이 방법을 통해 컴포넌트를 굉장히 유연하게 만들 수 있습니다. `onClick`과 `children` prop가 넘겨진 모습을 확인해보세요.


속성 펼치기 기법은 유용하게 사용될 수 있지만 **불필요한 props 혹은 틀린 어트리뷰트를 컴포넌트에 넘기게 되는 일이 생기기 쉽다**는 단점도 있습니다.

## JSX에서 자식 다루기

#### 1. 문자열 리터럴

여는 태그와 닫는 태그 사이에 문자열을 써넣을 수 있고, 이 때 `props.children`은 그냥 문자열이 됩니다.

1. 각 줄의 처음과 끝에 있는 공백을 제거합니다. 
1. 빈 줄이 삭제됩니다.
1. 태그에 붙어있는 개행이 삭제됩니다.
1. 문자열 리터럴 중간에 등장하는 여거래의 개행은 한개의 공백으로 줄어듭니다.

기본적으로, React에서는 cross-site-scripting(XSS) 공격을 막기 위하여 렌더링 되기 전에 JSX 내에 포함된 모든 값을 이스케이프 합니다. 따라서 모든 것은 렌더링 되기 전에 문자열로 변환됩니다.

`props.children`에서는 HTML 이스케이핑이 풀리게 되므로, 보통의 HTML을 사용할 수 있습니다.

![jsx의 이스케이프](https://bbgrams.github.io/assets/img/topic-5-jsx2.png)

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

![엘리먼트로 이루어진 배열](https://bbgrams.github.io/assets/img/topic-5-jsx3.png)

#### 3. JavaScript 표현식을 자식으로 사용하기

`{}`로 둘러싼 JavaScript 표현식은 모두 자식이 될 수 있습니다.
배열을 렌더링하고 싶을 때 자주 사용됩니다.


```js
function Item(props) {
  return <li>count {props.count}</li>;
}

function TodoList() {
  const todos = ['finish doc', 'submit pr', 'nag dan to review'];
  return (
    <ul>
      {todos.map((message) => <Item key={message} message={message} />)}
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
        {(index) => <div key={index}>This is item {index} in the list</div>}
      </Repeat>
    );
  }
}
```

![함수를 자식으로 사용하기](https://bbgrams.github.io/assets/img/topic-5-jsx4.png)
