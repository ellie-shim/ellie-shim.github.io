---
layout: post
title: "1주차 topic - 비동기"
subtitle: "siots"
categories: siots
tags: topic
comments: true
---

# 1주차 TOPIC - 비동기 프로그래밍

[비동기 프로그래밍](https://helloworldjavascript.net/pages/285-async.html)

## Motivation - 타이머 API

1. 함수를 특정 시간이 지난 뒤에 실행하는 `setTimeOut()` `clearTimeOut()`
1. 함수를 주기적으로 실행하는 `setInterval()` `clearInterval()`

- 보안 위험성을 이유로 권장되지 않는다.
- ms단위(1000ms = 1초)
- `setTimeOut()`, `setInterval()`은 **타이머 식별자**를 반환한다. 반환 값은 숫자이고, 타이머를 식별할 수 있는 0이 아닌 값이다.
- `setTimeout()`과 `setInterval()`는 같은 ID 공간을 공유하기 때문에, clearTimeout()과 clearInterval() 둘 중 어느 것을 사용해도 기술적으로 동일하게 동작한다.
  하지만 명확성을 위해, 코드를 유지보수할 때 혼란을 피하기 위해 항상 일치시켜야 한다.
- 정확한 지연시간을 보장해주지 않는다.

```js
const timeoutId = setTimeout(() => {
  alert("setTimeout이 실행된 지 2초가 지났습니다.");
}, 2000);
// setTimeout을 실행하면 timeoutId에 반환값(식별자)이 들어간다.

clearTimeout(timeoutId);
// clearTimeout으로 반환값(식별자)를 전달하면 타이머가 취소된다.
```

## 브라우저의 JavaScript 코드 실행과정

### 1. 호출 스택 (Call Stack)

함수의 실행 흐름이 왔다갔다 하는데 이 흐름을 스택형태로 관리한다.

모든 실행이 끝나면 호출 스택이 다 비워진다.

호출 스택에 작업이 하나라도 들어있으면 브라우저가 먹통이 된다.

자바스크립트 엔진이 관리하는 저장공간이다.

호출 스택에 저장되는 각 항목을 **실행 맥락(execution context)** 라고 하고 실행맥락에는 아래와 같은 정보들이 저장된다. - 함수 내부에서 사용되는 변수 - 스코프 체인 - `this가` 가리키는 객체

### 2. 작업 큐 (Task Queue)

작업을 저장하는 공간이다. 무언가 처리가 일어나진 않는다.

### 3. 이벤트 루프(event loop)

```js
// #1
console.log("Hello");
// #2
setTimeout(function() {
  console.log("Bye");
}, 3000);
// #3
console.log("Hello Again");
```

이벤트 루프는 콜 스택을 모니터하고 태스크 큐에서 수행할 작업이 있는지 확인하는 단일 스레드 루프이다. 콜 스택이 비어 있고 태스크 큐에 콜백 함수가 있는 경우, 함수는 큐에서 제외되고 실행될 콜 스택으로 푸시된다.

## 동기(Syncronous) 프로그래밍

실행되어야 할 행동이 세가지(디자인, 퍼블리싱, 스크립트)가 있을 때

1. 디자인 작업을 시작하고 1시간의 시간이 지난 후 **완료**한다
1. 퍼블리싱 작업을 시작하고 1시간의 시간이 지난 후 **완료**한다
1. 스크립트 작업을 시작하고 2시간의 시간이 지난 후 **완료**한다
1. 세가지 작업을 하는데 총 4시간의 시간이 소요됐다.

각각의 행동을 순차적으로 진행하고, 한가지 행동이 **완료되었을 때** 다음 행동을 진행한다.

## 비동기(Asyncronous) 프로그래밍

실행되어야 할 행동이 세가지(디자인, 퍼블리싱, 스크립트)가 있을 때

1. 디자이너에게 디자인를 진행하라고 명령한다.
1. 퍼블리셔에게 퍼블리싱를 진행하라고 명령한다.
1. 스크립터에게 스크립트를 진행하라고 명령한다.
1. 1시간이 지난 후 디자인과 퍼블리싱이 완료된다.
1. 2시간이 지난 후 스크립트가 완료된다.
1. 세가지 작업을 하는데 총 2시간의 시간이 소요됐다.

각각의 행동이 완료되기를 기다리지 않고 바로 다음 행동으로 넘어가는 방식.

행동마다 완료되는 시간이 다를 수 있다.

`자바스크립트의 비동기 처리란 특정 코드의 연산이 끝날 때까지 코드의 실행을 멈추지 않고 다음 코드를 먼저 실행하는 자바스크립트의 특성을 의미한다.`

### 1. 콜백(Callback)

다른 함수의 인수로 넘기는 함수

복잡한 비동기 작업을 할 수는 있지만 코드가 많이 복잡해진다 => 콜백 안의 콜백 안의 콜백 안의 .... 콜백 지옥(callback hell)

### 2. Promise

콜백의 문제점을 해결한 기능. ES2015에서 추가되었다.

자바스크립트 비동기 처리에 사용되는 객체

**'언젠가 끝나는 작업'의 결과값**을 담는 통이다. 작업이 끝난 후에 값이 채워진다.

- 비동기 작업을 하는 Promise 객체는 `Promise` 생성자를 통해 만들 수 있다.

  1. `Promise`생성자는 콜백을 인수로 받는다. 첫번째 인수로 `resolve` 가 들어오는데, 콜백 안에서 `resolve`를 호출하면 **`resolve`에 인수로 준 값이 곧 Promise 객체의 결과값이 된다.**

  1. 두번째 인수로는 `reject`가 들어온다 => 비동기 작업에서 에러가 발생했을 때 호출하는 함수

  1. `then` 메소드를 통해 콜백을 등록해서, 작업이 끝났을 때 결과값을 가지고 추가 작업을 할 수 있다.

  1. `then` 메소드 자체도 Promise객체를 반환한다. 콜백에서 반환한 값이 곧 Promise의 결과값이 된다.

  1. 비동기 작업을 연속해서 작업할 때 `then`을 이어붙여서 사용할 수 있다.(`then`메소드도 Promise를 반환하므로)

  1. 연이어 비동기 작업을 하는 코드를 깔끔하게 작성할 수 있다.

```javascript
function delay(ms, value) {
  return new Promise(resolve => {
    setImeout(() => {
      resolve(value); //resolve에 인수로 준 값이 promise 객체의 결과값이 된다.
    }, ms);
  });
}
// delay는 promise 통을 반환하는 함수이다.
// ms밀리세컨드의 시간이 지난 후 value를 반환한다.
// => delay(1000, 'hello')라고 함수를 호출하면 1초 뒤에 'hello'가 채워진 통이 반환된다.

delay(1000, "hello") // 1초 뒤에 'hello' 가 채워진 통이 반환된다
  .then(str => {
    // 위의 반환값이 then의 인수(str)에 들어간다
    return delay(2000, str + "world"); // str에 위의 반환값('hello')가 들어간 상태로 다시 함수가 실행된다. 이때의 결과값('hello world')이 채워진 통이 반환되고
  })
  .then(str => {
    // 위에서 반환된 값이 then의 인수(str)에 들어간다
    console.log(str);
  });
```

1. 함수를 호출하고 1초 뒤에 'hello'가 채워진 통이 반환된다.
1. 반환된 값을 이용해 콜백함수가 실행된다.
1. 2초 뒤에 'hello world'가 채워진 값이 반환된다.
1. 'hello world'가 콘솔창에 출력된다.

![promise 처리 흐름-출처:MDN](https://bbgrams.github.io/assets/img/docs/promise-flow.svg)

`promise 처리 흐름(출처 : mdn)`

#### HTTP 통신을 할 때

```javascript
axios
  .get(`${API_URL}/repos/facebookincubator/create-react-app/issues?per_page=5`) // 해당 주소에 get요청을 보내고 받은 데이터의 결과값이 담긴 통이 반환된다.
  .then(res => {
    // 받은 데이터가 res에 담긴다
    res.data
      .map(issue => issue.title)
      .forEach((title, index) => console.log(index + 1 + " : " + title));
  });
```

### 비동기 함수 (Async Function)

ES2017에 도입됐다.

함수 앞에 `async` 키워드를 붙이면 이 함수는 **비동기 함수**가 된다.

비동기 함수는 **항상 Promise 객체를 반환한다.** 이 Promise의 결과값은 비동기 함수 내에서 무엇을 반환하느냐에 따라 결정되며, **`then` 메소드와 똑같은 방식으로 동작한다.**

#### await

- 비동기함수 내에서 `await` 키워드를 사용할 수 있다.
- **`await` 뒤에 오는 Promise가 결과값을 가질 때까지 함수를 잠시 멈추고, Promise 통에 값이 채워지면 함수를 다시 실행하여 값을 반환한다** (비동기식으로 작동하기 때문에 브라우저는 Promise가 완료될 때까지 다른 작업을 처리할 수 있다.)
- `await`는 연산자이기도 하다.
- `await`의 값을 변수에 저장할 수 있다.
  ```javascript
  const str = await delay(3000, "hello");
  // 3초 뒤에 hello라는 값이 str에 저장된다.
  ```
- `await` 연산의 결과값은 뒤에 오는 Promise 객체의 결과값이 된다.
- `await`는 `for`, `if`와 같은 제어구문에서도 사용할 수 있다.
- `then` 메소드를 사용할 때 보다 **복잡한 비동기 데이터 흐름을 아주 쉽게 표현할 수 있다**

가장 큰 장점은 **동기식 코드를 짜듯이 비동기식 코드를 짤 수 있다**는 것이다.

```javascript
// Promise 객체를 반환하는 함수.
function delay(ms) {
  return new Promise(resolve => {
    setTimeout(() => {
      console.log(`${ms} 밀리초가 지났습니다.`);
      resolve();
    }, ms);
  });
}

async function main() {
  await delay(1000); // 1초 뒤에 결과값 반환
  await delay(2000); // 2초 뒤에 결과값 반환
  const result = await Promise.resolve("끝");
  console.log(result);
}

main();
```

```javascript
// 비동기 함수
async function func1() {
  //...
}

// 비동기 화살표 함수
const func2 = async () => {
  //...
};

// 비동기 메소드
class MyClass {
  async myMethod() {
    //...
  }
}
```

## 면접 문제

1. 동기와 비동기의 차이점을 설명하라
1. Promise란 무엇이며 코드가 어떻게 구성되어있는가
1. Promise와 Callback의 차이점은 무엇이며 각각의 장단점에 대해 설명하라
1. Async, Await가 무엇이며, 사용해본 경험이 있는가
1. 이벤트 루프란 무엇입니까?
