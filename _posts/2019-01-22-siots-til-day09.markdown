---
layout: post
title: "9일차 - 브라우저 동작원리, GraphQL, Testing, npm"
subtitle: "siotz"
categories: siotz
tags: til
comments: true
---

# 추후에 정리가 필요한 문서입니다!!!

# 9일차

1. 브라우저 동작원리
1. GraphQL
1. Testing
1. npm

# 1. 브라우저 동작 원리

## 1. 웹브라우저

## 2. 웹의 동작 원리

#### 부제: 브라우저 주소창에 www.google.com 을 쳤을 때 일어나는 일

우리는 `www.google.com` 이라고 주소창에 입력하고 확인하지만 사실은 주소는 이렇게 되어있진않다. 주소는 IP주소로 `198.61.190.241`라는 주소를 갖고있고 `google.com`은 우리가 볼 때 편하게 볼 수 있게 이름을 준것이다.

서버는 클라이언트에게 자료들 packet을 보내준다(패킷 : 작은 단위로 묶인 자료)

protocol : 언어의 규칙

# 2. REST

## 1. REST란?

- REpresentational State Transfer

- `HTTP URI`로 잘 표현된 리소스에 대한 행위를 `HTTP Method` 로 정의한다.

- `REST`는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일이다.

- `REST`는 네트워크 상에서 Client와 Server 사이의 통신 방식 중 하나이다.

## 2. REST API

## 3. RESTful

6가지 원칙을 잘 따라서 맞추면 RESTful하다. 라고 한다 (형용사처럼..)

## 4. REST의 장단점

### 장점

1. 2. 3.

### 단점

1. 2. 3.

#### graphQL과 비교했을 때의 단점

1. (보통의 경우) 각각의 자원마다 경로가 따로 있음. 즉, 여러 자원이 동시에 필요한 경우에는 요청을 여러 번 보내야 함 (요청의 횟수 면에서 비효율적) => user와 postlist 둘 다 가져오고 싶을떄는 embed등으로 묶여있지 않은경우엔 각각따로따로 두번 요청해서 가져와야한다

2. (보통의 경우) 자원의 필요한 속성만 얻어올 수 없음. 즉, 일부 속성이 필요하더라도 전체 속성을 가져와야만 함 (요청의 용량 면에서 비효율적) => user 테이블에서 id만 가져오고 싶은데 user를 가져오면 id 뿐만 아니라 id, password, 등등 필요없는것도 다 가져와서 데이터 비용이 든다.

# 3. GraphQL

# 4. 테스팅

개발에 있어서 엄청 중요!

## TDD 개발론

test 코드를 먼저 작성 한 후에 개발하는 것.

# 5. NPM

- Node Package Manager 

#### package.json