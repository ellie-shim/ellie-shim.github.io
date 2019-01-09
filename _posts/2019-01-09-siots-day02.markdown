---
layout: post
title: "2일차 - Iterable, 클래스, 비동기"
subtitle: "siots"
categories: siots
tags: til
comments: true
---

# 추후에 정리가 필요한 문서입니다!!!

# 2일차

1. 김시옷님의 Iterable, 클래스 강의
1. 심시옷님의 비동기 강의

## Iterable

### Iteration(이터레이션)

Iteration 프로토콜에는 두가지 프로토콜이 있다. 한가지는 `iterable 프로토콜`이고 또 다른 한가지는 `iterator 프로토콜`이다.

ES2015에서 추가된 이 두 가지는 새로운 빌트인 혹은 구문이 아닌 프로토콜 즉, 규약이다. 이들은 같은 규칙을 준수하는 객체에 의해 구현될 수 있다.

#### 순회가 가능하다는 성질을 가지고 있다 => 이터러블하다 ?

아래의 iterable이라는 객체인데 이 객체는 기본적으로 `symbol.iterator`라는 속성(property)을 가지고있다. iterator를 이용해서 이 객체가 순회를 할 수 있는 것이다.

- String
- Array
- TypedArray
- Map
- Set

```js
// iterable 객체를 만들어내는 생성자인 String
const str = "hello";
str[Symbol.iterator]; // [Function]

// Num
const num = 2;
num[Symbol.iterator];
// undefined
//
```

`symbol.iterator`라는 속성(property)을 가지고있지 않으면 이터러블 객체가 아니다.

### 1. Iterable의 사용

- for...of 루프
- spread 연산자(...)
- 분해대입
- 기타 iterable을 인수로 받는 함수

```js
// `for...of`
for (let c of "hello") {
  console.log(c);
}

// spread 연산자
const characters = [..."hello"];
//[ 'h', 'e', 'l', 'l', 'o' ]

// 분해대입
const [c1, c2] = "hello";
console.log(c1); // h

// `Array.from`은 iterable 혹은 array-like 객체를 인수로 받습니다.
Array.from("hello");

// split 방법
const characters1 = "hello".split("");
```

### 2. Generator 함수

#### 참고 링크

[Poiemaweb-es6-generator](https://poiemaweb.com/es6-generateor)

iterable 객체를 생성하는 함수.

generator 함수를 사용하면 무조건 iterable 객체를 반환한다.

반환된 그 객체는 iterable protocol을 만족한다. => 즉 `Symbol.iterator` 속성을 갖고있다.

```js
// generator 함수 선언하기
function* gen1() {
  //...
}

// 표현식으로 사용하기
const gen2 = function*() {
  //...
};

// 메소드 문법으로 사용하기
const obj = {
  *gen3() {
    //...
  }
};
```

```js
function* gen1() {
  //...
}

// `gen1`를 호출하면 iterable이 반환됩니다.
const iterable = gen1();

iterable[Symbol.iterator]; // [Function]
```

#### yield

Generator 함수 안에서 `yield` 라는 특별한 키워드를 사용할 수 있다.
Generator 함수 안에서 yield 키워드는 `return`과 유사한 역할을 하며, iterable의 기능을 사용할 때 yield 키워드 뒤에 있는 값들을 순서대로 넘겨준다.

```js
function* numberGen() {
  yield 1;
  yield 2;
  yield 3;
}

// 1, 2, 3이 순서대로 출력됩니다.
for (let n of numberGen()) {
  console.log(n);
}
```

`yield*` 표현식을 사용하면, 다른 generator 함수에서 넘겨준 값을 대신 넘겨줄 수도 있다.

```js
function* numberGen() {
  yield 1;
  yield 2;
  yield 3;
}

function* numberGen2() {
  yield* numberGen();
  yield* numberGen();
}

// 1, 2, 3, 1, 2, 3이 순서대로 출력됩니다.
for (let n of numberGen2()) {
  console.log(n);
}
```

`yield` 키워드를 제외하면, generator 함수 내부의 동작 방식은 일반적인 함수와 별반 다르지 않다. 즉, 다른 함수에서 할 수 있는 일이라면 generator 함수 안에서도 모두 할 수 있다

#### generator 함수를 사용할 때 주의점

- Generator 함수로 부터 생성된 iterable은 한 번만 사용될 수 있다. ( 한번 yield가 내려가면 다시 올라갈 수 없다)

  ```js
  // Generator 함수로부터 생성된 iterable은 한 번만 사용될 수 있습니다.
  function* gen() {
    yield 1;
    yield 2;
    yield 3;
  }

  const iter = gen();

  for (let n of iter) {
    // 잘 출력됩니다.
    console.log(n);
  }
  for (let n of iter) {
    // `iter`는 한 번 사용되었으므로, 이 코드는 실행되지 않습니다.
    console.log(n);
  }

  const iter2 = gen();

  for (let n of iter2) {
    // 잘 출력됩니다.
    console.log(n);
  }
  ```

- Generator 함수 내부에서 정의된 일반 함수에서는 yield 키워드를 사용할 수 없다.

#### generator 는 iterable 구현과 비동기 함수의 호출 차단 등에 유용합니다

### 3. Iterator Protocol

[이터레이션 프로토콜](https://gitlab.com/siots-study/topics/wikis/uploads/4b4f1f0a8e5d51b3315eac577e041561/iteration-protocol.png)

제너레이터 함수는 이터러블을 만드느 함수이다. 이터러블 객체 자체가 심볼.이터레이터를해서 가지고 있는게
이터러블이 가능하다는것은 심볼.이터레이터라는 속성을 가지고있는거니까.....
제너레이터 함수로 반환되는 것은 이터러블 객체이고, 이터러블 객체는

음..^^ 나중에 한번 더 봅시다.

이터레이터는 순회 가능한 자료 구조인 이터러블의 각 요소를 순회하기 위한 포인터로서 next 메소드를 갖는다. next 메소드는 value, done 프로퍼티를 갖는 객체(iterator result)를

iterator 객체 안의 메소드(next, done, value)를 사용하려면 방법이 두가지 있다.

1. 이터러블한 자료구조를 가지고있는 애한테 `[symbol.iterator]()`라는 메소드를 사용하면 iterator 객체가 반환된다. 그럼 이 iterator 객체 안의 next()를 사용할 수 있다.
1. generator 함수를 사용해서 이터러블한 객체를 만들어내면, 제너레이터가 알아서 iterator를 생성해주므로 next()등을 사용할 수 있다.

### 4. Generator와 Iterator

1. generator 함수로부터 만들어진 객체는 iterable protocol과 iterator protocol을 동시에 만족한다.

   ```js
   function* gen() {
     // ...
   }

   const genObj = gen();
   genObj[Symbol.iterator]().next === genObj.next; // true
   ```

1) generator 함수 안에서 return 키워드를 사용하면 반복이 바로 끝나면서 next 메소드에서 반환되는 객체의 속성에 앞의 반환값이 저장됩니다. 다만, return을 통해 반환된 값이 반복 절차에 포함되지는 않습니다.

1) generator 함수로부터 생성된 객체의 next 메소드에 인수를 주어서 호출하면, generator 함수가 멈췄던 부분의 yield 표현식의 결과값은 앞에서 받은 인수가 됩니다.

## 클래스

### 1. ES2015 class

ES2015 이전까지는 비슷한 종류 객체를 많이 만들어내기 위해 생성자를 사용해왔다(prototype)

ES2015에서 도입된 클래스는 생성자의 기능을 대체합니다. class 표현식을 사용하면, 생성자와 같은 기능을 하는 함수를 훨씬 더 깔끔한 문법으로 정의할 수 있습니다.

class는 prototype를 사용하는데 좀 더 쉽게 사용할 수 있도록 만들어졌다.

#### class는 별도의 문법으로 코드를 작성해야 한다. 함수나 객체처럼 작성해서는 안된다.

1. 객체에서는 콤마(,)가 있고, `class` 에서는 콤마(,)가 없다.
1. new
1. 정적메소드 : 생성자에 .찍고 사용하는 메소드(`Number.isNaN`,`Array.from`...)
1. 메소드를 다른 함수의 인수로 넘겨줘야 하는 경우 화살표 함수를 사용하는 것이 좋다.

문법이 아니라 동작방식의 측면에서 보면, ES2015 이전의 생성자와 ES2015의 클래스는 다음과 같은 차이점이 있습니다.

클래스는 함수로 호출될 수 없습니다.

클래스 선언은 let과 const처럼 블록 스코프에 선언되면, **호이스팅(hosting)**이 일어나지 않습니다.
클래스의 메소드 안에서 super키워드를 사용할 수 있습니다

class는 프로토타입을 좀 더 쓰기 쉽게 고안된 기능이다.

### 3. Class 정의

함수처럼 class 문법도 class 선언과 class 표현식 두가지 방법으로 정의가 가능합니다.

함수 선언과 달리 클래스 선언은 호이스팅이 일어나지 않기 때문에 클래스를 사용하기 위해서는 선언을 먼저 해주어야 한다.

class 선언식

```js
class People {
  constructor(name) {
    this.name = name;
  }

  say() {
    console.log("My name is " + this.name);
  }
}
```

class 표현식 - Class 표현식은 이름을 가질 수도 있고 갖지 않을 수도 있습니다

```js
const People = class People {
  constructor(name) {
    this.name = name;
  }

  say() {
    console.log("My name is " + this.name);
  }
};

const People = class {
  constructor(name) {
    this.name = name;
  }

  say() {
    console.log("My name is " + this.name);
  }
};
```

클래스를 이용해서 여러가지 객체를 찍어 낼 때, 공통의 변수를 줄 때 정적메소드를 이용한다.
=> 소나무, 단풍나무, 느티나무의 객체를 찍어 낼 떄, `나무`라는 공통 분모를 주고싶을 때

### 8. 클래스 상속
