---
layout: post
title: "4일차 - 객체, 프로토타입"
subtitle: "siotz"
categories: siotz
tags: til
comments: true
---

# 추후에 정리가 필요한 문서입니다!!!

# 4일차

1. 조시옷님의 객체, 프로토타입 강의

## 객체

#### 내장객체

이미 만들어져 있는 string, object 등..

#### 호스트 객체

브라우저 런타임환경에서 제공되는 객체

## 프로토타입 (Prototype)

> 프로토타입 들어가기 전에 읽어볼 것
> 함수를 정의하면 프로토타입이 속서응로 자동으로 생긴다. 이 프로토타입도 하나의 객체이다. 함수로 생성된 객체들은 이 프로토타입을 공유하고있다. 프로토타입에는 함수 뿐만 아니라 변수도 지정할 수 있다.

함수를 선언함과 동시에 프로토타입이 생긴다. (함수만)

[프로토타입 넌 이미 알고있다](https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67)

```js
const kim = new Person();
```

kim을 찍었을때 나오는 `__proto__` 은 Prototype Link이다. 자기를 만든 원형 객체의 프로토타입을 가리킨다.

#### 인스턴스

프로토타입으로 만들어진 객체 말고, 본래의 생성자 속성을 복사해서 만들어진(메모리를 차지하는) 애들을 인스턴스라고 하는거같다..

#### 정적 메소드(static method)

스태틱으로 메소드를 선언하면 프로토타입이 아니고 함수 객체 쪽에 생성이 되는데, 얘는 한번 선언하면 수정은 할 수 없고 나중에 가져다가 쓸수만 있다.

#### 비공개 스태틱

```js
var Gadget = (function() {
  // 스태틱 변수/프로퍼티
  var counter = 0; // 생성자의 새로운 구현 버전을 반환한다.
  return function() {
    console.log((counter += 1));
  };
})(); // 즉시 실행한다.
```

위의 코드에서 생성자는 첫번째 함수가 아니고 return 뒤의 반환되는 함수가 생성자이다! 그래서 counter에 접근할 수 없어서 비공개 스태틱이다 ????

[출처 Web Club](http://webclub.tistory.com/526)
