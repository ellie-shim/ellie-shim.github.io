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

속성 펼치기 기법은 유용하게 사용될 수 있지만 **불필요한 props 혹은 틀린 어트리뷰트를 컴포넌트에 넘기게 되는 일이 생기기 쉽다**는 단점도 있습니다.

## JSX에서 자식 다루기


