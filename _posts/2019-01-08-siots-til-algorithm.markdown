---
layout: post
title: "자료구조"
subtitle: "siots"
categories: siots
tags: til
comments: true
---

#자료구조론

## 스택, 큐

[큐, 스택](https://helloworldjavascript.net/pages/282-data-structures.html)

### 스택 Stack

배열로 되어있는 자료구조

LIFO(Last In First Out) - 후입선출 => 스택은 리포다.

웹브라우저에서 history를 읽을 때 사용된다.

DFS에서 사용됨.

- 번외
  1. 배열에 아무것도 없을 때 top = -1
  1. 배열에 아이템이 1개 있을 때 top = 0
  1. 배열에 아이템이 2개 있을 때 top = 1
  1. peek()의 값은 top과 같다.

#### 자바스크립트에서의 스택

**콜스택(호출스택)**

자바스크립트 엔진은 **함수 호출과 관련된 정보를 콜스택**에서 관리한다.

호출 스택에 저장되는 각 항목을 실행 맥락(excution context) 라고 한다.

실행맥락에는

- 함수 내부에서 사용되는 변수
- 스코프 체인
- `this`가 가리키는 객체
  가 저장된다.

**호출스택에 실행 맥락이 존재하는동안, 즉 실행 중인 함수가 존재하는 동안**에 브라우저는 먹통이 된다.

### 큐 Queue

위아래가 뚫려있는 구조

FIFO(First In First Out) - 선입선출

in : enqueue, insert

out : dequeue, delete

큐는 피포이다.

컴퓨터 시스템에서 가장 많이 쓰인다.

예) 여러가지 문서를 출력할 때 먼저 출력 버튼을 누른 문서부터 출력된다.

BFS에서 사용됨.

순서대로 처리해야하는 작업을 임시로 저장해두는 버퍼로서 많이 사용된다.(작업 큐)

#### 자바스크립트에서의 큐

**태스크 큐(작업 큐)**

작업을 저장하는 공간이다. 무언가 처리가 일어나진 않는다.

##
