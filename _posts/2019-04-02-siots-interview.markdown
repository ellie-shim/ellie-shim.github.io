---
layout: post
title: "면접질문 정리해보기 2"
subtitle: "siotz"
categories: siotz
tags: interview
comments: true
---

1. 고차함수 ?

- 함수를 인수로 받는 함수 또는 함수를 반환하는 함수입니다. 함수를 인수로 받는 함수엔 forEach, map, reduce, filter 등이 있고 함수를 반환하는 함수에는 bind가 있습니다.

1. 콜백 함수?

- 다른 함수의 인수로 넘겨지는 함수입니다.

1. 클로저 ?

- 바깥 함수 스코프의 변수를 안쪽 함수에서 사용하는 것입니다. 변수를 보호하는 작업을 할 수 있어서 데이터 보존이나 접근 권한 제어에 사용합니다.

1. 저장소로서의 클로저 코딩

   ```js
   // 전역변수 사용을 방지하기 위해 클로저를 사용할 수 있는데 아래와 같이 작성하면
   // 전역에 작성되진 않지만 모두가 가져다가 사용할 수 있다.
   function closure() {
     const a = 1;
     const b = 2;
     return { a, b };
   }
   const obj = closure();
   obj.a; // 1
   obj.b; // 2
   ```

1. 클로저 코딩 2

   ```js
   function closure() {
     let title = "help";
     return {
       getTitle: function() {
         return title;
       },
       setTitle: function(movie) {
         title = movie;
       }
     };
   }
   const movie = closure();
   movie.getTitle(); // help
   movie.setTitle("titanic");
   movie.getTitle(); // titanic
   ```

1. 재귀함수 ?

- 함수 내부에서 자기 자신을 호출하는 함수입니다.

1. 재귀함수의 문제점?

- 잘못짜면 무한루프에 빠질 수 있고,
  재귀호출의 깊이가 깊어질 수록 메모리에 부담이 가기 때문에 깊은 구조에서는 지양하는 것이 좋습니다.

1. 객체란?

- 키와 값 쌍으로 이루어진 데이터들의 뭉치입니다.

1. 얕은 복사? 깊은 복사?

- 객체나 배열같은 참조타입을 복사할 때에는 데이터 자체가 복사되는 것이 아니라 데이터가 담겨있는 곳을 가리키는 참조를 복사합니다. 그래서 얕은 복사가 일어나고, 배열안의 배열이나 객체 안의 객체 같은 중첩된 내부 객체는 복사되지 않습니다. 깊은 복사를 하려면 immutable.js 이나 immer를 사용할 수 있습니다.

1. 빠른 연산 ?

- && : 왼쪽 피연산자가 falsy이면 왼쪽 값을 바로 반환합니다. 아니라면 오른쪽 피연산자의 결과값을 반환합니다.
- || : 왼쪽 피연산자가 truthy이면 왼쪽 값을 바로 반환합니다. 아니라면 오른쪽 피연산자의 결과값을 반환합니다.

1. ==, ===?

- == : 비교할 두 대상의 타입이 다르면 타입을 변환한 후에 비교합니다. null 체크를 할때 사용합니다.
- === : 비교할 두 대상의 타입이 다르면 무조건 false를 반환합니다.
