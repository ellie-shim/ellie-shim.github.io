---
layout: post
title: "3주차 topic - Axios, fetch API"
subtitle: "siots"
categories: siots
tags: topic
comments: true
---

# 3주차 TOPIC - Axios, fetch API

## 1. Axios

### 1. Axios ?

**Promise 기반**의 HTTP 통신 라이브러리

상대적으로 다른 HTTP 통신 라이브러리들에 비해 문서화가 잘 되어있고 API가 다양하다.

여러 편의기능(instance와 같이 설정을 재사용하거나 요청중인 연결을 취소하는 등)을 제공

TypeScript를 사용할 수 있다

> axios는 내부적으로 XMLHttpRequest를 사용하고 있는데 Service Worker 등의 최신 기술이 XMLHttpRequest를 지원하지 않으므로, Service Worker를 사용할 예정에 있는 프로젝트에서는 Axios 대신 Fetch API를 사용해야만 함

---

### 2. 설치 방법

CDN 방식과 NPM 방식 2가지가 있다.

#### CDN 방식

```js
<script src="https://unpkg.com/axios/dist/axios.min.js" />
```

#### NPM 방식

```bash
npm install axios
```

---

### 3. 추가 방법

컴포넌트 파일에 axios를 가져온다.

```js
import axios from "axios";
```

---

### 4. IE에서의 axios

_axios는 promise 기반이라고 했지요 ?_

`IE`는 promise가 지원되지 않기 때문에 `axios`를 사용할 수 없다. _충격적.._

`es6-promise` 패키지를 설치하여 해결할 수 있다.

#### 설치

```bash
npm install — save es6-promise
```

#### es6-promise 추가

```js
require(‘es6-promise’).polyfill();
```

---

### 5. axios 사용

`axios()` 메소드를 사용한다.

결과값은 `promise`를 반환한다.

`axios`는 반환된 응답을 `JSON`으로 변환시켜 주고, 자바스크립트에서 `data` 객체로 반환된다. => 반환된 데이터 구조 그대로 사용이 가능하다.

---
