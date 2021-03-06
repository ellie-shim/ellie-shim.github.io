---
layout: post
title: "1일차 - 자료구조론, "
subtitle: "siotz"
categories: siotz
tags: til
comments: true
---

# 추후에 정리가 필요한 문서입니다!!!

# 1일차

1. 조시옷님의 알고리즘 강의
1. 조시옷님의 심화1 강의

## 알고리즘 강의(자료구조론 part1)

### 큐, 스택

[큐, 스택](https://helloworldjavascript.net/pages/282-data-structures.html)

#### 스택 Stack

배열로 되어있는 자료구조

LIFO(Last In First Out) - 후입선출 => 스택은 리포다.

웹브라우저에서 history를 읽을 때 사용된다.

DFS에서 사용됨.

**콜스택(호출스택)** 자바스크립트 엔진은 **함수 호출과 관련된 정보를 콜스택**에서 관리한다.

- 번외
  1. 배열에 아무것도 없을 때 top = -1
  1. 배열에 아이템이 1개 있을 때 top = 0
  1. 배열에 아이템이 2개 있을 때 top = 1
  1. peek()의 값은 top과 같다.

#### 큐 Queue

위아래가 뚫려있는 구조

FIFO(First In First Out) - 선입선출

in : enqueue, insert

out : dequeue, delete

큐는 피포이다.

컴퓨터 시스템에서 가장 많이 쓰인다.

예) 여러가지 문서를 출력할 때 먼저 출력 버튼을 누른 문서부터 출력된다.

BFS에서 사용됨.

순서대로 처리해야하는 작업을 임시로 저장해두는 버퍼로서 많이 사용된다.(작업 큐)

## 심화1

[심화 1](https://helloworldjavascript.net/pages/220-value-in-depth.html)

### 값 더 알아보기

#### const와 let의 차이

- let은 재대입 가능. const는 불가.
- const는 선언과 대입을 동시에 해줘야한다.
- let은 선언 따로, 대입 따로도 가능하다

#### const와 let의 공통점

- let과 const 둘 다 같은 이름을 갖는 변수의 재선언을 허용하지 않는다.
- 변수가 선언되기 전에 참조하려고 하면 에러가 난다.
- 블록 스코프를 갖는다.

#### var vs let, const

- var는 재선언할 수 있다.
- let, const 는 블록 스코프, var는 함수 스코프를 갖는다.★★

#### scope란 ?

- 현재 접근할 수 있는 변수들의 범위
- 현재 위치에서 볼 수 있는 변수들의 범위

어떠한 변수가 스코프 안에 선언되었으면 해당 스코프 안에서는 변수에 접근해서 읽거나 쓸 수 있고, 스코프 밖에서는 해당 변수에 접근할 수 없다.

- [scope가 조금 다른 catch](https://repl.it/@bbgrams/IdealisticTestyBrain)
- catch 와 with의 예외 - 관심있는 사람은 각자 찾아볼 것.
  catch 와 with의 경우 인자로 포함되는 error / inScope등의 변수들은 scope 안에서만 사용가능하나 그 내부에서 선언한 변수들은 global scope를 따른다.
- catch는 조금 다른 스코프를 갖는다.

#### 함수 scope 와 블록 scope 란?

- 함수 scop는 함수 단위로 범위를 지정한다.
- 블록 scope 는 중괄호{} 단위로 범위를 지정한다.

- [function scope 예제](https://repl.it/@bbgrams/functionScope)
- [block scope 예제](https://repl.it/@bbgrams/blockScope)

#### 호이스팅

var 변수의 선언부를 제일 위로 끌어 올린다. 선언부만!
let, const 변수는 호이스팅 기능이 없다.

- 함수가 함수 선언식(function declaration)으로 선언되면, 현재 스코프의 최상단으로 호이스팅(hoist) 된다.
- 함수 또는 var로 선언된 변수
- var는 함수 스코프이기 때문에 함수 내부에서 맨 상단으로 끌어올려짐.

```js
// This is the same as the one below
sayHello();
function sayHello() {
  console.log("Hello!");
}
// This is the same as the code above
function sayHello() {
  console.log("Hello!");
}
sayHello();
```

- 반면 함수가 함수 표현식(function expression)으로 선언되면, 함수는 현재 스코프의 최상단으로 호이스팅되지 않는다.

- `var`를 이용해서 선언해도, 선언부만 상단부로 올라가기때문에 함수는 실행되지않는다.

```js
sayHello(); // Error, sayHello is not defined
const sayHello = function() {
  console.log(aFunction);
};
```

- [함께 읽어볼 호이스팅 심화 자료](https://gist.github.com/LeoHeo/7c2a2a6dbcf80becaaa1e61e90091e5d)
- 개인 심화자료 - [let과 const는 호이스팅이 될까?](https://medium.com/korbit-engineering/let%EA%B3%BC-const%EB%8A%94-%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85-%EB%90%A0%EA%B9%8C-72fcf2fac365)
- 함수를 선언과 동시에 실행하는 [IIFE](http://jw910911.tistory.com/m/21)

#### 네스팅된 스코프(Nested scopes)에서의 렉시컬 스코핑(lexical scoping)

함수가 다른 함수 내부에서 정의되었다면, 내부 함수는 외부 함수의 변수에 접근할 수 있다. 이런 행동을 렉시컬 스코핑(lexical scoping)이라고 부른다.

```js
function outerFunction() {
  const outer = "I’m the outer function!";

  function innerFunction() {
    const inner = "I’m the inner function!";
    console.log(outer); // I’m the outer function!
  }

  console.log(inner); // Error, inner is not defined
}
```

#### 글로벌 변수(전역변수)를 사용하면 안되는 이유

- [글로벌 변수 선언 예시](https://repl.it/@bbgrams/globalVariables)

1. 간혹 다른 라이브러리를 사용하거나, 큰 프로젝트 소스를 나누어서 관리할 때 충돌이 일어날 수 있어서

2. 서버의 중요한 데이터나 공개하고 싶지 않은 데이터를 처리할 때 (즉, 해킹이나 보안적 측면)

- 브라우저에는 기본적으로 자바스크립트 콘솔이나 디버깅 툴이 내장되어 있으므로 이를 이용하면 소스는 기본이고, 자바스크립트 변수값들도 쉽게 알아낼 수 있다.

3. 메모리 관리 측면

- [자바스크립트에서 메모리 누수의 4가지 형태](https://itstory.tk/entry/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%97%90%EC%84%9C-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%88%84%EC%88%98%EC%9D%98-4%EA%B0%80%EC%A7%80-%ED%98%95%ED%83%9C)

예방방법

1. 클로저 이용
2. 모듈화
3. 엄격모드 이용 (엄격모드 - 엄격하게 문법을 검사하겠다. 전역 변수 사용 못하게 함) - [strict mode](https://beomy.tistory.com/13)

#### 전역 객체 window

전역 객체가 뭔지, 특징들만 알고 넘어가도 될 듯.

- 자바스크립트의 특징은 글로별 영역도 하나의 변수로 정의하여 사용하고 있다는 점이다. 그게 window.
- 전역 객체는 단 하나만 유일하게 존재
- 어떤 컨텍스트가 실행되기 전에 먼저 생성됨
- 내부적으로 생성자가 없기 때문에 new를 이용해서 생성자로서 이용할 수 없다.
- window 객체는 글로벌 변수로 선언한 모든 변수를 속성으로 갖는다.
- [쉽게 적어놓은 window 객체](https://www.zerocho.com/category/JavaScript/post/573b321aa54b5e8427432946)

### 참조

JavaScript에는 7가지의 타입이 존재한다.

- Boolean
- Null
- Undefined
- Number
- String
- Symbol
- Object

#### 원시타입(Primitive Type)과 참조타입(Reference Type)

원시타입 : 값을 그대로 할당 - Number, String, Boolean, null, undefined, Symbol

참조타입 : 값이 저장된 주소값을 할당(참조) - Object(Array, Function, RegExp)

- 원시타입은 값을 수정할 수 없다. (불변성)
- 문자열의 경우 조금 다른데, 문자열을 수정하는 모든 메서드들은 새로운 문자열을 반환한다.
- 원시타입은 값으로 비교됨.

- 참조타입은 값으로 비교되지 않는다. 참조로 비교된다.

- 원시 타입일 때에는 값이 복사되어 전달되지만, 참조 타입일 때에는 참조가 복사되어 전달된다.

- [자바스크립트 기본형과 참조형의 종류 및 차이점](http://officialslings.com/today-i-learned/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EA%B8%B0%EB%B3%B8%ED%98%95%EA%B3%BC-%EC%B0%B8%EC%A1%B0%ED%98%95%EC%9D%98-%EC%A2%85%EB%A5%98-%EB%B0%8F-%EC%B0%A8%EC%9D%B4%EC%A0%90/)

#### 객체의 같음(Equality)

주소값(참조)을 비교하기때문에 두 객체의 비교 연산은 `false`가 된다.

#### 불변성(Immutability)

> 원시 타입의 값 자체의 내용을 변경할 수 있는 방법은 없습니다. 이런 성질을 불변성(immutability)이라고 하고, "JavaScript의 원시 값은 불변(immutable)이다"라고 말합니다.

> 변수에 저장된 원시 타입의 값을 바꾸려면, 오직 변수에 다른 값을 대입하는 방법밖에 없습니다.

객체는 가변(mutable)이다. 이 가변성때문에 프로그래밍이 어려워지기도 한다.
객체를 얼려서(`Object.freeze`) 속성의 추가/변경/삭제를 막거나, Immutable 라이브러리를 사용하기도 한다.

##### const와 불변의 차이를 기억해두자★★★

- `const`는 '한번 초기화 된 변수에 다른값을 대입 할 수 없다.'
- 불변성은 '값 자체가 변하지 않는다'

#### 래퍼 객체(Wrapper Object)

javascript에서 문자열을 표현 하는 방법은 대표적으로 두가지가 있다.

```js
let str1 = new String("str1"); // new(생성자)를 이용해서 선언했기 때문에 객체가 된다.
let str2 = "str2";
```

위 표현방법의 차이는 typeof 연산자와 instanceof 연산자에서 드러난다.

```js
typeof str1; // 'object'
typeof str2; // 'string'

str1 instanceof String; // true
str2 instanceof String; // false

str1 instanceof Object; // true
str2 instanceof Object; // false
```

str1 변수는 String 함수에 의해 생성된 객체이므로 instanceof의 연산자의 작동에서는 문제될것이 없다.
다만, 'str2' 값은 리터럴로 생성된 primitive value 즉, 원시값으로 기본데이터이며 불변값이다. 다만 str2 변수와 str1 변수를 사용할때는 (String method를 사용하는 등) 차이가 없는데 그 이유는 primitive value를 사용할때는 Primitive wrapper objects로 감싸져서 사용되기 때문이다.
다만, primitive type의 문자열형태를 출력하는 typeof 연산자 혹은 객체에 대한 클래스 혹은 부모클래스를 판별하는 instanceof 연산자의 경우에는 사용 결과에 차이가 나게 된다.

원시타입의 값에 대해 속성을 읽으려고 시도하면, 그 값은 그 순간에만 객체로 변환되어 **마치 객체인것처럼 동작한다** => 객체에서만 사용할 수 있는 메소드를 사용할 수 있다.

### 함수 더 알아보기

#### this

- 내 과거 파일 참조

현재 실행 문맥을 가리킨다. 실행 문맥은 호출자가 누구냐 하는 것과 같다. 하지만, 전역 문맥에서는 window를 가리킨다. 주의.
예방할 수 있는 방법은 엄격모드. window를 가리키게 되지 않고 undefined가 된다.

> 그러면 엄격 모드를 사용하기 위해 매번 'use strict';를 직접 써주어야 할까요? 다행히도 그렇지는 않습니다. ES2015 모듈을 이용해 작성된 코드는 항상 엄격 모드로 동작하기 때문에, 함수 위에 'use strict';를 붙여주지 않아도 엄격 모드로 동작합니다.

- [MDN this](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this)

#### 주인없는 this

...

#### this 바꿔치기

##### bind, apply, call

this를 우리가 원하는 값으로 바꿔치기할 때 사용.

this가 가리키는 객체를 `실행 context`라고 한다.

- 셋 다 context를 조정한다.
- `call()` 과 `apply()`는 기능은 동일하지만 인수를 넘겨주는 형식에만 차이가 있다.
- call(), apply() 는 바로 호출하고, bind()는 바로 호출하지 않는다.
- call()은 파라미터를 콤마로 구분해서 일일이 넣어준다.
- apply()는 파라미터를 배열로 넘긴다.

```js
function printGrade(grade) {
  console.log(`${this.name} 님의 점수는 ${grade}점입니다.`);
}

const student = { name: "Mary" };
const printGradeForMary = printGrade.bind(student); // bind를 해줘도 바로 호출되지 않고 묶어만 놓는다. 밑에서 한번 더 호출해주어야 된다.

printGradeForMary(100); // Mary 님의 점수는 100점입니다.
```

- [bind, apply, call 간단 차이](http://officialslings.com/today-i-learned/bind-apply-%EA%B7%B8%EB%A6%AC%EA%B3%A0-call-%EB%A9%94%EC%86%8C%EB%93%9C%EC%97%90-%EB%8C%80%ED%95%9C-%EC%A0%95%EB%A6%AC/)
  어려움... 누가 알려줘...

- 심화 - [this는 어렵지 않습니다.](https://blueshw.github.io/2018/03/12/this/)

#### 화살표 함수

- ES6(ES2015)에 추가되었다.

- 화살표 함수의 장점은 축약도 축약이지만 **화살표 함수로 정의된 메소드를 다른 함수의 인수로 넘겨도 아무런 문제가 없다는 점.** 그렇지 않은 일반 function 인 경우 bind로 this를 묶어줘야함. 화살표 함수는 자신의 실행 context의 this를 받는다.

- 화살표 함수의 this는 호출될 때 결정된다.

- 화살표 함수에 call, apply는 아예 작동되지 않아서 this를 바꾸려해도 아무런 효과가 없다.

> 기존 자바스크립트에서 this는 dynamic scoping 이 되었는데 이 경우 lexical scoping을 사용하게 된다. 고로 따로 binding을 사용하지 않아도 된다. 정리하면 자신만의 this를 생성하지 않고 자신을 포함하고 있는 context의 this를 이어 받습니다.

- [화살표 함수와 this - 강사님 예제](https://repl.it/@bbgrams/arrow-function-this-1)

- [고급 특징](https://beomy.tistory.com/19)

- 화살표 함수는 일종의 익명함수
  _화살표 함수와 일반함수와의 차이점은?_
- 화살표 함수는 객체 생성자로 사용할 수 없다. 즉, new 연산자를 못 쓴다.
- this값 - 화살표 함수는 this 값을 현재 문맥에 바인딩시킨다. 일반 함수는 바인딩하지 않는다.
  따라서 화살표 함수에는 bind, call, apply가 먹히지 않는다.

#### arguments와 나머지 매개변수(Rest Parameters)

매개변수가 몇개 들어오는지 모를때 argument를 사용한다.
ES2015에서 추가된 나머지 매개변수 문법을 통해 똑같은 기능을 구현할 수 있다.

```js
function sum(...ns) {
  let result = 0;
  for (let item of ns) {
    result += item;
  }
  return result;
}

sum(1, 2, 3, 4); // 10
```

#### 매개변수의 기본값 (Default Parameter)

### 함수형 프로그래밍

#### 고차함수(HOC)

- 함수를 인수로 받는 함수 ex) map, reduce...
- 함수를 반환하는 함수 ex) bind
- 다른 함수의 인수로 넘겨지는 함수를 **콜백(callback)**이라고 부른다.

#### 클로저(Closure)

- 특정 함수가 참조하는 변수들이 선언된 렉시컬 스코프(스코프 위로 올라가는것)는 계속 유지되는데, 그 함수와 스코프를 묶어서 클로저라고 한다.
- 클로저가 나타나는 가장 기본적인 환경은 함수 안에 함수가 선언되었을 때. 즉, 스코프 안에 스코프가 있을 때.

```js
function outer() {
  let count = 0;
  let inner = function() {
    return ++count;
  };
  return inner;
}
let increase = outer();

console.log(increase()); // 1
console.log(increase()); // 2
```

즉, 클로저는 outer()와 같은 외부 함수에서 inner와 같은 내부 함수를 반환하여 다른 곳에서 해당 함수를 호출할 때 발생한다는 것을 알 수 있다.

### 클로저는 언제 사용할까?

- 자바스크립트 라이브러리나 모듈에서 private으로 나의 변수를 보호하고 싶을 때. 즉, 지역 변수 보호
- static 변수를 이용하고 싶을 때
- 데이터 보존 및 활용
- 접근 권한 제어

위와 같이 함수로 한번 둘러싸는 경우 가장 많이 사용하는 것이 바로 라이브러리일 것이다. 라이브러리일 때 뿐만아니라 사용자의 접근을 제한하고, 변수의 조작을 불가능하게 하기 위해서는 필수로 위와 같은 방법을 사용해야한다. 하지만 이것보다도 더 큰 이유는 바로 다른 라이브러리들과 함께 사용되는 경우 서로간 충돌을 없애기 위해 반드시 해야한다. 전역변수를 사용했다가 다른 라이브러리 가져왔는데 그 라이브러리에서 덮어씌워버린다면 이유도 모르고 멀쩡하던 웹 페이지에서 에러가 발생하게 될 것이다.

- [클로저 간단 예제](https://repl.it/@bbgrams/closure)
- [클로저의 정의 등 관련 내용- 클로저를 통한 은닉화](https://hyunseob.github.io/2016/08/30/javascript-closure/)

### 클로저 사용 시 주의할 점

- 클로저는 메모리를 소모한다.

-[출처](https://medium.com/@khwsc1/%EB%B2%88%EC%97%AD-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%8A%A4%EC%BD%94%ED%94%84%EC%99%80-%ED%81%B4%EB%A1%9C%EC%A0%80-javascript-scope-and-closures-8d402c976d19)

- ## private하게 쓰고싶은 변수는 앞에 언더바(\_)를 붙여주는것이 관례이다.(ex: \_name)

### 연산자 더 알아보기

#### 표현식

값으로 변환될 수 있는 부분을 표현식이라고 한다.

#### Short-circuit Evaluation

```js
false && expression;
true || expression;
```

#### 삼항 연산자(Ternary Operator)

#### Symbol

#### Map

#### Set

집합 형태의 자료구조. 객체이다.

중복된 데이터를 허용하지 않는다.

순서X, 중복된 데이터X 인 배열과 유사한 자료구조.

### 면접 질문

1. 클로저가 무엇이고 왜 쓰는지 설명하고 간단하게 코드로 구현해보아라.

함수 안에 함수가 있을 때 바깥 스코프에 있는 변수를 가져다 사용하는 내부 함수와,
변수가 저장되는 저장소를 클로저라고 한다. 변수를 프라이빗하게 쓰거나, 데이터를 숨기고 정해진 방법을 통해서만 데이터에 접근할 수 있도록 제한을 둘 때 사용된다.

```js
function movie(title) {
  let _title = title;
  return {
    getTitle: function() {
      return title;
    },
    setTitle: function() {
      return (title = _title);
    }
  };
}

const harry = movie("harryPotter");
const mid = movie("mmd");
console.log(harry.getTitle());
console.log(harry.setTitle("hrpt"));
console.log(harry.getTitle());
console.log(mid.getTitle());
```

2. 불변성이 무엇이며 이를 해결하기 위한 방법을 제시하라.

3. 화살표 함수와 일반함수와의 차이점은?

- 화살표 함수는 객체 생성자로 사용할 수 없다. (new 연산자를 사용할 수 없다)
- 화살표 함수는 this 값을 현재 문맥에 바인딩시킨다. => bind(), call(), apply()가 먹히지 않는다.
- 일반함수는 바인딩하지않아서 직접 bind() 해주어야한다.

4. 자바스크립트에서 this는 무엇인지?

```
   전역 공간에서 window
   함수 내부에서 window
   메소드 호출 시 메소드 호출 주체(a.p()를 하면 여기서 this는 a를 가리킨다.)
   콜백에서 window - 하지만 this를 명시하거나 this를 바인딩해서 넘기면 그에 따른다.
   생성자 함수에서 인스턴스
```

- [자바스크립트 this 바인딩](https://medium.com/@shlee1353/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-this-%ED%82%A4%EC%9B%8C%EB%93%9C-b748a732d55c)

5. == 와 === 차이

==연산자는 동등 연산자로, 피연산자가 서로 다른 타입이면 타입을 강제로 변환하여 비교한다. 하지만 형 변환이 어떻게 되는지 하나하나 외워서 사용하는 것은 복잡하기만 할 뿐이다.
===연산자는 일치 연산자로, 두 피연산자를 더 정확하게 비교한다. 형 변환을 하지 않고 비교.

6. 호이스팅이란?

   - function foo() {}와 var foo = function() {} 사이에서 foo 사용법의 차이에 대해 설명하시오.

7. let, var 또는 const를 사용하여 생성된 변수들의 차이점은 무엇인가요?

8. Function.prototype.bind에 대해 설명하시오.

- 호출될 때 그 this 키워드를 제공된 값으로 설정한다.
  => 일반 함수의 this를 고정시킬 때 사용한다.

9. 엄격모드가 무엇이고 어떻게 사용하는 것이지?

10. 고차 함수의 정의는 무엇입니까?

11. 자바스크립트 원시타입은 몇 개이고 전부 말하라.

---

###

- [개발자가 필히 알아야 할 ES6 10가지 기능](https://blog.asamaru.net/2017/08/14/top-10-es6-features/)

- [함수선언식과 함수표현식](https://joshua1988.github.io/web-development/javascript/function-expressions-vs-declarations/)

-[면접 질문 정리글-호주 미드급 개발자](https://medium.com/@jimkimau/%EC%9D%B4%EB%B2%88-%EA%B8%B0%EC%88%A0-%EB%A9%B4%EC%A0%91-%EC%A4%91-%EA%B8%B0%EC%96%B5%EB%82%98%EB%8A%94-%EC%A7%88%EB%AC%B8%EA%B3%BC-%EB%8B%B5%EB%B3%80%EB%93%A4-712daa9a2dc)

-[면접 질문 정리글2](https://github.com/JaeYeopHan/Interview_Question_for_Beginner#%EB%A9%B4%EC%A0%91%EC%97%90%EC%84%9C-%EB%B0%9B%EC%95%98%EB%8D%98-%EC%A7%88%EB%AC%B8%EB%93%A4)

-[면접 질문 정리글3](https://github.com/yangshun/front-end-interview-handbook/blob/master/Translations/Korean/questions/javascript-questions.md)
