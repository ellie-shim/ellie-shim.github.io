---
layout: post
title: "TypeScript - 1. 타입스크립트 소개"
subtitle: "타입스크립트"
categories: dev
tags: dev
comments: true
---

## 정적 타이핑과 동적 타이핑

### 1. 정적 타이핑(Static/Strong typing)

정적 타이핑은 실행 전 컴파일 과정에서 자료형을 결정하는 것 입니다. 변수 선언시 변수에 저장할 값의 자료형을 미리 설정해주어야 합니다. 컴파일 시에 자료형에 맞지 않는 값이 들어있으면 컴파일 에러가 발생합니다.

C, C++, C#, Java, swift 등이 있습니다.

컴파일 시에 타입에 대한 정보를 결정하기 때문에 속도가 빠르고, 실행 전에도 타입 관련 버그를 발견할 수 있습니다.

하지만 사용이 어렵습니다.

```c
char c = "ellie";
int num = 20;
```

### 2. 동적 타이핑(Dynamic/Weak typing)

동적 타이핑은 컴파일 시에 자료형을 결정하지 않고 실행 시에 결정합니다.

JavaScript, Ruby, Python 등이 있습니다.

배우기는 쉬우나 실행 전에는 타입 관련 버그를 발견하기가 어렵습니다. 실행 도중에 변수에 예상하지 못한 타입이 들어와 타입 에러를 뿜는 경우가 생길 수 있습니다.

```js
const str = "ellie";
const num = 20;
```

### 3. 정적 타입 체커

JavaScript에 `컴파일 과정 중 타입 체크 기능`을 추가한 확장 언어입니다.

코드를 실행하기 전에 타입 관련 버그를 찾아낼 수 있는 기술입니다.

TypeScript와 Flow가 있습니다.

## TypeScript

TypeScript는 자바스크립트의 슈퍼셋인 프로그래밍 언어입니다. 마이크로소프트에서 개발, 유지하고 있습니다.
TypeScript는 JavaScript의 ES5 문법을 그대로 사용할 수 있습니다. 또한, Babel과 같은 트랜스파일러를 사용하지 않아도 ES6의 새로운 기능을 기존의 자바스크립트 엔진에서 실행할 수 있습니다.

### 1. TypeScript의 장점

#### 1.1 정적 타입

정적 타입 체커인 TypeScript는 자바스크립트의 코드에 타입(자료형)을 사전에 지정하여 작성할 수 있습니다. 때문에 컴파일 단계에서 버그를 확인할 수 있습니다.

명시적인 정적 타입 지정은 개발자의 의도를 명확하게 코드로 작성할 수 있고, 이는 코드의 가독성을 높이고 예측할 수 있게하며 디버깅을 쉽게 합니다.

```js
function sum(a: number, b: number) {
  return a + b;
}

sum("x", "y"); //error
```

#### 1.2 도구의 지원

IDE(통합개발환경)를 포함한 다양한 도구의 지원을 받을 수 있습니다. IDE와 같은 도구에 타입 정보를 제공함으로써 높은 수준의 인텔리센스(IntelliSense), 코드 어시스트, 타입 체크, 리팩토링 등을 지원받을 수 있으며 이러한 도구의 지원은 대규모 프로젝트를 위한 필수 요소이기도 합니다.

## 참고

[Poiemaweb-Typescript 소개](https://poiemaweb.com/typescript-introduction)
