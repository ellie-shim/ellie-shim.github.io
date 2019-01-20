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

**Promise 기반**의 HTTP 통신 라이브러리 => `axios`의 리턴 값은 `Promise`

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

> jsonp, CORS, ...아롸보좌

#### 참고 링크

[axios-ajax 비동기 작업 처리](https://beomy.tistory.com/36)

## 2. fetch API

[FetchAPI와 XHR의 차이점이 모냐??](https://stackoverflow.com/questions/35549547/what-is-the-difference-between-the-fetch-api-and-xmlhttprequest)

```md
#### 자꾸 헷갈려

웹페이지 전체를 리로드하지 않고 일부분만을 리로드하고 비동기식으로 데이터를 불러와 작업하는 `XMLHttpRequest` 객체

초기에는 XHR을 이용해서 AJAX 요청을 보냈다.

하지만 IE가 판치던 그 옛날, IE에서 AJAX 요청을 보내기가 까다로워서 `jquery AJAX`나 `axios`, `superagent`같은 라이브러리를 사용했다.

XHR을 좀 더 유연하게 사용할 수 있는 것이 `fetch API`?

fetch와 XHR 둘 다 서버에 ajax 요청을 할 수 있다.
fetch 에는 XHR에서 사용할 수 없는 몇가지 추가 기능이 있다.
fetch폴리필에서
```

- ajax를 구현하는 여러가지 방법 중 최신 방법이 fetchAPI이다

* 비교적 최근에 도입되어 `IE` 및 구형 안드로이드 브라우저(4.x)는 지원하지 않음.

  - Chrome
  - FireFox
  - Safari 6.1+
  - Internet Explorer 10+

* `fetch()`는 `Promise`를 반환한다.

> Axios는 XHR을 사용하는데, `Service Worker`등의 최신 기술이 XHR을 지원하지 않으므로 Service worker를 사용할 예정이라면 Fetch API를 사용해야 함

### 1. Service Worker

[서비스 워커가 무엇이죠](https://medium.com/@Dongmin_Jang/frontend-service-worker-%EC%84%9C%EB%B9%84%EC%8A%A4-%EC%9B%8C%EC%BB%A4%EA%B0%80-%EB%AC%B4%EC%97%87-2dab5d60f611)

- 오프라인 상황에서 브라우저가 뭘 해야될지 개발자가 제어할 수 있도록 한 것.

- 브라우저가 백그라운드에서 실행하는 스크립트로 웹페이지와는 별개로 작동한다.

- **주기적 백그라운드 동기화** 가능 : 오프라인으로 인해서 특정 처리가 완료되지 못했을 때, 온라인 상태가 되면 자동으로 처리가 완료되는 것(채팅)
- **푸시알림 가능** : sns에 올린 글에 대한 알림이 브라우저 알림으로 뜨는 것(페이스북)

> ajax에선 뭐가 안된다고 했었죠 ?

#### 주의할 점

1. 보안상의 이유로 https를 통해서만 실행된다. => 개발중에 `localhost`를 이용해서 서비스워커를 사용할 수 있지만 사이트에 배포하려면 서버에 https 설정을 해야한다.
1. 표준이 아니다
1. Promise 사용법을 알아야한다.
1. 모든 브라우저를 지원하지 않는다.

#### 참고 링크

[Service Worker - MDN](https://developer.mozilla.org/ko/docs/Web/API/Service_Worker_API)

[Service Worker 소개 - 구글](https://developers.google.com/web/fundamentals/primers/service-workers/?hl=ko)

[Service Worker 지원 브라우저](https://jakearchibald.github.io/isserviceworkerready/)

---

#### 참고 링크

[MDN-fetch API](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API)

[MDN-Using FetchAPI](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API/Fetch%EC%9D%98_%EC%82%AC%EC%9A%A9%EB%B2%95)

[fetch-polyfill](https://github.com/github/fetch)

[fetchAPI와 async-await](https://developers.google.com/web/fundamentals/primers/async-functions?hl=ko)

## 3. Polyfill

### 1. polyfill ?

개발자가 특정 기능이 지원되지 않는 브라우저를 위해 사용할 수 있는 코드 조각이나 플러그인을 말한다. 폴리필은 보통 HTML5 및 CSS3와 오래된 브라우저 사이의 간격을 메꾸는 역할을 담당한다.

---

#### 참고 링크

[Modernizr-HTML5 Cross Browser Polyfills : 개발되어있는 폴리필을 모아놓은 페이지](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills)
