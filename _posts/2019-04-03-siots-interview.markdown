---
layout: post
title: "면접질문 정리해보기 3"
subtitle: "siotz"
categories: siotz
tags: interview
comments: true
---

1. prototype?

- 자주 사용되는 메소드나 속성을 저장한 객체입니다. 원하는 속성이나 메소드를 상속해주는 방법으로 재사용 할 수 있습니다.

- 사전적인 정의는 객체가 만들어질 때의 객체 자신의 본연의 모습이라고 정의가 내려져있는데,
  객체가 만들어 질 때 같이 생성되는 프로토타입이라는 객체가 있는데 반복적으로 사용되는 속성이나 메소드들을 이 프로토타입에 넣어서 사용할 수 있습니다.

- 객체가 생성될때 같이 만들어지는 객체의 원형, 자기 자신이라고 할 수 있습니다.

1. 상속? 체인?

- 객체의 속성에 접근 할 때 객체의 프로토타입까지 확인해 보고 해당 속성이 없으면 그 프로토타입의 프로토타입을 확인해봅니다. 이런식으로 프로토타입의 프로토타입의 프로토타입..을 확인하는 것을 프로토타입 체인이라고 합니다.

- 객체 리터럴로 만든 객체의 프로토타입의 끝은 object이고 이 object의 프로토타입은 null입니다.

- 자바스크립트가 프로토타입 기반 언어라 다른 클래스 기반 언어의 상속 기능을 흉내내려고 나온 것입니다. 실제 상속된다기보다는 부모 프로토타입의 속성을 공유하여 쓴다고 할 수 있습니다. 타고타고 올라가서 null이 나올때까지 타고 올라갑니다.

- 자바스크립트는 다른 언어처럼 클래스의 상속으로 구성된 것이 아니어서, 프로토타입을 이용하는데 이 프로토타입은 상속이라기보다는 부모의 속성을 공유하는 느낌으로 사용되는 것이어서 체인이 가능합니다.

1. 정적 메소드란?

- 생성자의 속성에 직접 지정된 메소드입니다.
- 다른 인스턴스에 대한 요소가 아닌 자기 자신을 위한 메소드입니다.

1. 분해대입을 손코딩 해보세요.

```js
```

1. 프로토타입 코딩 1

```js
"안녕".sayStr(); // 을 했을 떄 콘솔에 안녕이 출력되게 해보세요
```

1. 프로토타입 코딩 2

   - 객체 리터럴.
   - 초기값은 0.
   - count.inc(); 증가
   - count.red(); 감소

1. 프로토타입 코딩 3

   - 2번 문제를 생성자 함수로 작성

1. 프로토타입 코딩 4

   - 생성자 함수로
   - 초기값은 0
   - 입력값을 받을 수 있도록

1. 프로토타입 코딩 5

   - 클래스로 작성

1. 프로토타입 코딩 6

   - 프로토타입 체인에 대한 코드를 작성하고 설명.

1.

```js
// 1.
String.prototype.saystr = function() {
  console.log(this.toString());
};
"안녕ㅎㅎ".saystr();

// 2.
// - 객체 리터럴.
// - 초기값은 0.
// - count.inc(); 증가
// - count.red(); 감소
const count = {
  num: 0,
  inc: function() {
    return console.log(++this.num);
  },
  red: function() {
    return console.log(--this.num);
  }
};
count.inc();
count.red();

// 3 .
// - 2번 문제를 생성자 함수로 작성
function Count() {
  this.num = 0;
}
Count.prototype.inc = function() {
  return console.log(++this.num);
};
Count.prototype.red = function() {
  return console.log(--this.num);
};
const count = new Count();
count.inc();
count.red();

// 4.
function Count() {
  this.num = 0;
  this.inc = function(c = 1) {
    this.num += c;
    return console.log(this.num);
  };
  this.red = function(c = 1) {
    this.num -= c;
    return console.log(this.num);
  };
}
const count = new Count();
count.red(10);

// 5. 클래스를 이용해서
class Count {
  constructor(num) {
    this.num = 0;
  }
  inc(c = 1) {
    this.num += c;
    return this.num;
  }
  red(c = 1) {
    this.num -= c;
    return this.num;
  }
}
const count = new Count();
count.inc(10);

//6
const obj1 = {
  a: 1
};
const obj2 = {
  b: 2
};
const obj3 = {
  c: 3
};
Object.setPrototypeOf(obj2, obj1); // setPrototypeOf는 시간이 좀 걸릴 수 있음.
Object.setPrototypeOf(obj3, obj2);
const obj4 = Object.create(obj1);

console.log(obj3.a);
console.log(obj3.b);
console.log(obj3.a);
console.log(obj4.a);
```
