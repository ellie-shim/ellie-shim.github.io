---
layout: post
title: "5주차- REACT - 2 "
subtitle: "siots"
categories: siots
tags: topic
comments: true
---

# 5주차 topic - REACT - 타입 체크

# Proptypes를 이용한 타입 체크

> React v15.5부터 React.PropTypes 는 별도 패키지로 옮겨졌습니다. 대신 [prop-types 라이브러리](https://www.npmjs.com/package/prop-types)를 사용하시길 바랍니다.

위의 라이브러리를 이용하여 
컴포넌트의 props을 체크할 수 있습니다.

prop에 유효하지 않은 값이 전달되면 콘솔에 경고가 노출됩니다.

#### 1. PropTypes

```js
import PropTypes from 'prop-types';

class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

Greeting.propTypes = {
  name: PropTypes.string
};
```

`Greeting` 컴포넌트의 `props.name`의 타입을 `string`으로 설정해주었습니다.

#### 2. 단일 자식 요구하기

```js
import PropTypes from 'prop-types';

class MyComponent extends React.Component {
  render() {
    // This must be exactly one element or it will warn.
    const children = this.props.children;
    return (
      <div>
        {children}
      </div>
    );
  }
}

MyComponent.propTypes = {
  children: PropTypes.element.isRequired
};
```

`PropTypes.element.isRequired`를 사용하면 하나의 컴포넌트만 자식으로써 전달되게 할 수 있습니다.

#### 3. 기본 Prop 값

```js
class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

// Specifies the default values for props:
Greeting.defaultProps = {
  name: 'Stranger'
};
```

`defaultProps` 속성을 이용하여 props의 기본값을 설정할 수 있습니다.

# 정적 타입(자료형) 체크

#### 1. 정적 타이핑

- (실행 전) 컴파일 과정에 타입을 검사합니다.
- 실행 전에도 타입관련 버그를 발견 할 수 있습니다. => 컴파일 시에 타입에 대한 정보를 결정하기 때문에 속도가 빠릅니다.
- 타입 에러로 인한 문제점을 초기에 발견할 수 있어 타입의 안정성이 높습니다.
- 하지만 사용이 어렵습니다.
- C, C++, C#, JAVA, swift, 코틀린
- `int num = 1;`, `bool isLoading = false;`
    

#### 2. 동적 타이핑

- 실행시간에 타입을 검사합니다.  => 실행 도중에 변수에 예상치 못한 타입이 들어와 타입에러를 뿜는 경우가 생길 수 있습니다.
- 실행 전에는 타입관련 버그를 발견하기 어렵습니다. 
- 루비, 파이썬, JavaScript

#### 3. 정적 타입 체커

- JavaScript에 `컴파일 과정 중 타입 체크 기능`을 추가한 확장 언어
- 코드를 실행하기 전에 타입관련 버그를 찾아낼 수 있는 기술.
- TypeScript(더 많이 씀), Flow(페이스북 개발)

정적 타입 체커는 코드를 실행하기 전에 몇몇 문제를 식별합니다. 자동 완성같은 기능을 추가하여 개발자의 작업흐름을 개선하기도 합니다.

이런 이유로 큰 코드 베이스에서는 상단의 `PropTypes` 대신 Flow나 TypeScript 사용을 권장합니다.
