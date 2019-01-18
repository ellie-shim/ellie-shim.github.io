---
layout: post
title: "8일차 - 자바스크립트 엔진"
subtitle: "siots"
categories: siots
tags: til
comments: true
---

# 추후에 정리가 필요한 문서입니다!!!

# 8일차

1. 안시옷님의 모듈 심화, 바벨

# 1. 모듈

## 1. 모듈을 정의하는 방법

### 1. 객체 리터럴(Object Literal)

### 2. 모듈 패턴(Module Pattern)

디자인 패턴 (좋은 코드들의 패턴들을 공식?정석?처럼 정해놓고 이름을 붙여놓는것)중 하나이다

객체를 어떻게 예쁘게 구조화 할 것인지

네임스페이스 : 자기만의 이름을 가지고 있는 공간?

```js
const Module = (function() {
  // Module이라는 네임스페이스를 가졌다.
  // code
})();
```

#### Privacy & Private Method

##### Privacy

클로저를 이용해서 private하게 만들 수 있는데 이러한 성질을 privacy하다라고 한다.

##### Private method

private 메소드는 이렇게 모듈 스코프 안에서 보호되고, 이 메소드가 위치한 스코프 외부에서 다른 사용자 / 개발자 / 헤커들이 해당 메소드를 보거나, 호출할 수 없게하는 메소드입니다. 우리는 이미 모듈 스코프를 생성했습니다. 이 모듈 스코프 안에서 private 메소드를 어떻게 정의하는지 그 기본적인 형태를 먼저 보겠습니다.

#### 모듈 객체 설정 문법

### 3. 노출식 모듈 패턴 (Revealing Module Pattern)

이걸 가장 많이 쓴다고 하는 듯!

## 2. 모듈 포맷

자바스크립트가 아닌, 다른 일반 영리한 개발자들이 만든 문법
