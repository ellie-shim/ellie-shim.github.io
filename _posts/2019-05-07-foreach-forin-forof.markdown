---
layout: post
title: "forEach, for in, for of 비교"
subtitle: "forEach, for in, for of"
categories: dev
tags: dev
comments: true
---

## map, set

map과 set은 ES6(ES2015)에서 추가된 자료구조입니다.

### map

map은 key-value 형태로 key는 중복되지 않는 특징을 가집니다.

```js
let map = new Map();

map.set("name", "ellie");
map.set("age", 28);
map.set("age", 29);

console.log(map); // Map { 'name' => 'ellie', 'age' => 29 }
```

age 값에 여러번 set을 해주어도, 가장 마지막에 set한 값만 유지됩니다.

### set

set은 값의 집합인데, 배열과 다르게 중복 된 값을 가지지 않습니다.

```js
let set = new Set();

set.add(1);
set.add(2);
set.add(3);
set.add("3"); // string
set.add(1);

console.log(set); // Set { 1, 2, 3, '3' }
```

set에 같은 값을 여러번 add 해주어도 중복 된 값은 무시합니다.

## 예제 데이터

```js
const map = new Map();
map.set("name", "ellie");
map.set("age", 29);

const set = new Set();
set.add(1);
set.add(2);
set.add(3);

const arr = [1, 2, 3];

const obj = { name: "ellie", age: 29 };
```

## forEach

배열에서 사용 가능한 반복문입니다. ES6부터는 map, set에서도 지원됩니다.

인자로 콜백함수를 등록할 수 있고, 배열의 각 요소들이 반복될 때 콜백함수가 호출됩니다.

콜백함수에서 배열 요소의 key(index)와 value에 접근할 수 있습니다.

```js
function forEachFunc(map, set, arr, obj) {
  function loopFunc(value, index) {
    console.log(`${value},,,${index}`);
  }
  console.log("==map==");
  map.forEach(loopFunc);
  console.log("==set==");

  set.forEach(loopFunc);
  console.log("==arr==");

  arr.forEach(loopFunc);
  console.log("==obj==");

  obj.forEach(loopFunc);
}
forEachFunc(map, set, arr, obj);
```

![forEach 결과값 확인](https://ellie-shim.github.io/assets/img/forEachloop.png)

- map 에서는 **key-value 출력**
- set 에서는 value, index 상관없이 **value 출력**
- array 에서는 **value, index 출력**
- **object 에서는 forEach가 동작하지 않습니다.**

## for in

`for in` 반복문은 모든 객체에서 사용이 가능합니다. 객체의 key 값에만 접근이 가능합니다.(value 값 접근 불가)

객체 자신의 속성 및 상속 받은 속성 중 열거 가능한(enumerable) 속성(객체의 enumerable 속성이 true로 설정 된 속성)의 이름을 배열로 반환합니다.

```js
function forInFunc(map, set, arr, obj) {
  console.log("==map==");
  for (const i in map) {
    console.log(i);
  }

  console.log("==set==");
  for (const i in set) {
    console.log(i);
  }

  console.log("==arr==");
  for (const i in arr) {
    console.log(i);
  }

  console.log("==obj==");
  for (const i in obj) {
    console.log(i);
  }
}

forInFunc(map, set, arr, obj);
```

![for in 결과값 확인](https://ellie-shim.github.io/assets/img/forinloop.png)

- array, object의 key 값이 출력됩니다.
- map, set은 enumerable 속성이 false 이기 때문에 for in 반복문이 동작하지 않습니다.

## for of

ES6에 새로 추가된 반복문입니다. 해당 구문을 사용하기 위해선 [Symbol.iterator] 속성을 가지고 있어야 합니다.(직접 명시 가능)

이 속성 안에 어떠한 함수가 들어있다면 `반복 가능한 객체(iterable object)` 혹은 `iterable` 이라고 하고, 해당 객체는 iterable protocol을 만족한다고 합니다.

내장 된 생성자 중 iterable 객체를 만들어내는 생성자는 아래와 같은 것들이 있습니다.

- String
- Array
- TypedArray
- Map
- Set

```js
function forOfFunc(map, set, arr, obj) {
  console.log("==map==");
  for (const i of map) {
    console.log(i);
  }

  console.log("==set==");
  for (const i of set) {
    console.log(i);
  }

  console.log("==arr==");
  for (const i of arr) {
    console.log(i);
  }

  console.log("==obj==");
  for (const i of obj) {
    console.log(i);
  }
}
forOfFunc(map, set, arr, obj);
```

![for of 결과값 확인](https://ellie-shim.github.io/assets/img/forofloop.png)

- map 에서는 [key, value] 를 출력했습니다.
- set, Array 에서는 value를 출력했습니다.
- object는 [Symbol.iterator] 속성이 비어있기 때문에 iterable for of 구문이 작동하지 않습니다.

## forEach, for ..in, for ..of 의 속도 차이

[http://jsben.ch/BQhED](http://jsben.ch/BQhED)에서 확인해봤을 때 for구문이 가장 빠르다고 확인됩니다

---

#### 참고

- [forEach, for in, for of 특징 및 성능 비교](https://medium.com/sjk5766/foreach-for-in-for-of-%ED%8A%B9%EC%A7%95-%EB%B0%8F-%EC%84%B1%EB%8A%A5-%EB%B9%84%EA%B5%90-47a77464b034)
- [자바스크립트 for in cs for of 반복문 정리](https://jsdev.kr/t/for-in-vs-for-of/2938/1)
- [자바스크립트로 만나는 세상](https://helloworldjavascript.net/pages/175-control-statement.html)
