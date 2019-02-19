---
layout: post
title: "20일차 - Immer"
subtitle: "siots"
categories: siots
tags: til
comments: true
---

# 추후에 정리가 필요한 문서입니다!!!

# 20일차

# ImmutableJS와 Immer

## 불변성 (Immutability)

원시타입의 값 자체의 내용을 변경할 수 없다 => 불변성


## ImmutableJS

완전한 자바스크립트가 아니다. 자바스크립트라이브러리지만 자바스크립트가 아니다..그래서 좀 변환하는 귀찮은 작업이 있다.

`toJS`로 변환


## Immer

`produce` 함수만 알면 된다!!

draft 는 현재 상태(todos)의 복사본이라고 할 수 있다. 이 draft에 push등을 해서 draft를 수정할 수 있고 produce의 반환값은 producer에서 수정된 draft의 반환값이다..(?)

원본 todos는 보존되면서 바뀐 상태가 nextTodos가 된다.

이제 RECEIVE_PRODUCTS가 실제로 무엇을 하는 놈인지 쉽게 이해 가는지 보이지 않나여? 코드가 많이 깔끔해졌고, default 케이스에 대한 처리도 필요가 없어졌다. 드래프트에 변경을 가하지 않으면 기본 상태가 그대로 반환되니께>< => draft는 원래 상태의 복사본이니까 ! switch에서 걸리지 않으면 draft가 그대로 반환되므로 원래 상태가 그대로 반환된다 그래서 default 처리가 없어도 된다 오오~~~

# Hooks

클래스 컴포넌트와 함수형 컴포넌트가 있는데 
클래스 컴포넌트에만 있는 기능이 있었다.(state,등)

Hook을 이용해서 함수형 컴포넌트에서도 state를 쓸 수 있다.

Hook은 새로운 기능이 아니라 새로운 선택권정도로 볼 수 있다.

필수는 아니란 말!

`useState(0)` 는 상태값의 기본값을 설정해주는건데, 상태들의 defaultState값을 0이라고 설정해주는것이다 

`const [value, setValue] = useState(0);`
value는 state의 키고, 0은 value라는 상태의 초기값이다. setValue는 value를 setState하는 함수이다. `[상태키, 상태를 변경하는 함수명?]` 을 세트로 만들어주는 것이 문법.


그래서 훅은? Hook은 함수 컴포넌트에서 React state와 생명주기 기능을 "연동(hook into)"할 수 있게 해주는 함수다. 그래서 hook은 class 안에서 사용할 수 없다. 

#### Effect Hook: useEffect

컴포넌트가 마운트 되거나 업데이트 될 때 렌더링된다.

#### Custom Hook

HOC 없이 Hook을 이용해서 로딩인디케이터를 만들 수 있다.

[![Edit react-hooks](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/ykj1ylzrqx)

# React Router

#### Redirect
화면을 이동하면 히스토리에 추가되는게 아니고 주소가 덮어씌워져서 히스토리에 남지 않는다. 그래서 뒤로가기가 안됨. push를 줘서 덮어씌우는게 아닌 새로 생성돼서 넘어가게 한다. 뭔가 문제가 나올것이니 나중에 확인해보자.


#### StaticRouter
리액트를 서버사이드 렌더링으로 짤 때 쓰는 라우터

#### Switch
