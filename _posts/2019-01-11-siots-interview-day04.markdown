---
layout: post
title: "면접 질문 - 4일차(20190111) "
subtitle: "siotz"
categories: siotz
tags: interview
comments: true
---

#### 객체

1. 객체
1. 프로토타입

---

1.

1. function Person(){}
2. var person = Person()
3. var person = new Person() 의 차이점은 무엇입니까?

```
1) 함수 선언식, 일반 함수를 선언한다. Person()이라는 함수 선언부가 호이스팅 된다.
2) Person 함수의 실행값을 person이라는 변수에 담는다.
3) new 생성자를 이용해서 Person의 instance를 만들고 person은 이 instance를 담는다.
```

2. 호스트 객체와 내장 객체의 차이점은 무엇입니까?

```
내장객체 : 자바스크립트 내부에 이미 만들어져있는 객체(Object, function, array, string ..등)
호스트객체 : 브라우저 런타임환경에서 제공되는 객체
```

3. 프로토타입 상속이 어떻게 작동하는지 설명하세요.

```
프로토타입은 상속받는다기보다는, 프로토타입을 공유한다고 할 수 있다.
객체에 속성이 없을 때 그 객체의 프로토타입에서 해당 속성을 찾아보고, 또 그 프로토타입에서 해당 속성을 찾아보며 위로위로 올라갈 수 있다.
```
