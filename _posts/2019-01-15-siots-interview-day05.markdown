---
layout: post
title: "면접 질문 - 5일차(20190115) "
subtitle: "siots"
categories: siots
tags: interview
comments: true
---

#### DOM

---

#### 1. DOM에 대해서 설명하세요.

```
Document Object Model의 약자로 웹페이지를 제어하는 모델이다.
HTML 웹문서를 파싱한 것을 DOM이라고 한다.
```

#### 1. 이벤트 위임에 대해 설명하세요.

```
이벤트 버블링의 특성을 이용해 하위요소에 각각 이벤트를 붙이지 않고 상위 요소에서 하위 요소의 이벤트를 제어하는 방식이다.
```

#### 1. event bubbling과 event capturing에 대해 설명하세요.

```
이벤트 버블링 : 특정 요소에서 이벤트가 발생했을 때 해당 이벤트가 더 상위의 요소들로 전달되어가는 특성

이벤트 캡쳐링 : 특성 요소에서 이벤트가 발생했을 때 최상위 요소에서 해당 이벤트가 발생한 요소까지 탐색하는 특성
```

#### 1. preventDefault와 stopPropagation의 차이점에 대해 설명하세요.

```
preventDefault() : 어떠한 태그의 기본 이벤트 동작을 취소한다.
stopPropagation() : 이벤트 전파(버블링, 캡쳐링)를 중단한다.
```

#### 1. [추억의 문제] mouseover, mouseout 과 mouseenter, mouseleave의 차이점 - 추억하고 싶지 않지만 추억해 봅시다!

```
mouseover, mouseout 은 이벤트 버블링이 일어나고
mouseenter, mouseleave는 이벤트 버블링이 일어나지 않는다.
```
