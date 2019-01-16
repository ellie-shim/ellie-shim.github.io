---
layout: post
title: "5일차 - DOM"
subtitle: "siots"
categories: siots
tags: til
comments: true
---

# 추후에 정리가 필요한 문서입니다!!!

# 5일차

1. 조시옷님의 DOM

## BOM (Browser object Model) : 브라우저 객체 모델

브라우저를 제어하는 객체 모델 (브라우저의 기능-엑스버튼이나,,등등)

## DOM (Document object Model) : 문서 객체 모델

웹페이지를 제어하는 객체 모델

> HTML은 HTML웹문서이고, DOM은 HTML 웹문서를 파싱한것이다.

htmlcollection 태그로 포함되는 node만 포함되고
nodeList는 모든 node를 포함한다

[HTMLcollection과 nodeList의 차이](http://www.code.i-harness.com/ko-kr/q/f0879e)

## 이벤트

## 이벤트 전파

Capturing 과 Bubbling

#### 1. 이벤트 버블링 - event bubbling

이벤트 버블링은 특정 요소에서 이벤트가 발생했을 때 **해당 이벤트가 더 상위의 요소들로 전달되어 가는 특성**이다.

form 관련된 이벤트(submit.. 이런애들)들은 버블링이 일어나지 않는다.

default는 버블링!

#### 2. 이벤트 캡쳐링 - event captureing

capture에 true를 주면 캡쳐링이 일어나고
false를 주면 버블링이 일어나는데
기본값은 false(버블링)이다.

> 버블링과 캡쳐링은 항상 일어나는데 일어날때 **동작** 하는 것을 둘 중 하나를 선택해 줄 수 있다(capture : true 이런식으로해서.)

> 버블링과 캡쳐링은 항상 일어나는데 버블링일때 이벤트를 동작 할 것이냐, 캡쳐링일때 이벤트를 동작할 것이냐를 선택할 수 있다.
