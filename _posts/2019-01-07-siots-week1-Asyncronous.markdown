---
layout: post
title: "1주차 topic - 비동기"
subtitle: "siots"
categories: siots
tags: topic
comments: true
---

## 1주차 TOPIC - 비동기 프로그래밍

[비동기 프로그래밍](https://helloworldjavascript.net/pages/285-async.html)

## 브라우저의 JavaScript 코드 실행과정

### 1. 호출 스택 (Call Stack)

함수의 실행 흐름이 왔다갔다 하는데 이 흐름을 스택형태로 관리한다.

모든 실행이 끝나면 호출 스택이 다 비워진다.

호출 스택에 작업이 하나라도 들어있으면 브라우저가 먹통이 된다.

자바스크립트 엔진이 관리하는 저장공간이다.

### 2. 작업 큐 (Task Queue)

작업을 저장하는 공간이다. 무언가 처리가 일어나진 않는다.

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

### 1. 콜백(Callback)

다른 함수의 인수로 넘기는 함수

복잡한 비동기 작업을 할 수는 있지만 코드가 많이 복잡해진다 => 콜백 안의 콜백 안의 콜백 안의 .... 콜백 지옥(callback hell)

### 2. Promise

콜백의 문제점을 해결한 기능. ES2015에서 추가되었다.

**'언젠가 끝나는 작업'의 결과값**을 담는 통이다. 작업이 끝난 후에 값이 채워진다.

- 비동기 작업을 하는 Promise 객체는 `Promise` 생성자를 통해 만들 수 있다.

  1. `Promise`생성자는 콜백을 인수로 받는다. 첫번째 인수로 `resolve` 가 들어오는데, 콜백 안에서 `resolve`를 호출하면 **`resolve`에 인수로 준 값이 곧 Promise 객체의 결과값이 된다.**

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
