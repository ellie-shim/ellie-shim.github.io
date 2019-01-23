---
layout: post
title: "3주차 topic - Axios, fetch API"
subtitle: "siots"
categories: siots
tags: topic
comments: true
---

# 3주차 TOPIC - Axios, fetch API, Polyfill

## 1. Axios

### 1. Axios ?

**Promise 기반**의 HTTP 통신 라이브러리 => `axios`의 리턴 값은 `Promise`

상대적으로 다른 HTTP 통신 라이브러리들에 비해 문서화가 잘 되어있고 API가 다양합니다.

여러 편의기능(instance와 같이 설정을 재사용하거나 요청중인 연결을 취소하는 등)을 제공합니다.

TypeScript를 사용할 수 있습니다.

> axios는 내부적으로 XMLHttpRequest를 사용하고 있는데 Service Worker 등의 최신 기술이 XMLHttpRequest를 지원하지 않으므로, Service Worker를 사용할 예정에 있는 프로젝트에서는 Axios 대신 Fetch API를 사용해야만 함

---

### 2. 설치 방법

CDN 방식과 NPM 방식 2가지가 있습니다.

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

`IE`는 promise가 지원되지 않기 때문에 `axios`를 사용할 수 없다고합니다. _충격적.._

하지만 `es6-promise` 패키지를 설치하여 해결할 수 있습니다!

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

`axios()` 메소드를 사용합니다.

결과값은 `promise`를 반환합니다.

`axios`는 반환된 응답을 `JSON`으로 변환시켜 주고, 자바스크립트에서 `data` 객체로 반환된다. => 반환된 데이터 구조 그대로 사용이 가능하다. 우리가 그동안 분해대입을 사용해서 쉽게 코딩 할 수 있었던 것은 `axios`의 편리한 기능이었습니다!

#### GET

```js
const axios = require("axios");

function ax() {
  axios
    .get("https://jsonplaceholder.typicode.com/posts/1")
    .then(res => console.log(res));
}

async function ax() {
  const { data } = await axios.get(
    "https://jsonplaceholder.typicode.com/posts/1"
  );
  console.log(data);

  const {
    data: { title }
  } = await axios.get("https://jsonplaceholder.typicode.com/posts/1");
  console.log(title);
}
```

`res`에 응답객체가 들어옵니다. repl에서 응답 객체를 확인해보아요

#### POST

```js
const axios = require("axios");

function ap() {
  axios
    .post("https://jsonplaceholder.typicode.com/posts", {
      firstName: "Fred",
      lastName: "Flintstone"
    })
    .then(console.log(res));
}
```

#### 여러 요청 한번에 받기

```js
async function post1() {
  const {
    data: { title }
  } = await axios.get("https://jsonplaceholder.typicode.com/posts/1");
  return title;
}

async function post2() {
  const {
    data: { title }
  } = await axios.get("https://jsonplaceholder.typicode.com/posts/2");
  return title;
}

axios.all([post1(), post2()]).then(
  axios.spread(function(tit1, tit2) {
    console.log(tit1);
    console.log(tit2);
  })
);
```

axios.all을 하면 인수로 들어간 요청의 결과값이 담긴 promise가 반환됩니다.
이 promise에 then 콜백을 붙일 수 있습니다.

---

#### 참고 링크

[Axios 공식문서-Github(영문)](https://github.com/axios/axios#cancellation)

[axios-ajax 비동기 작업 처리](https://beomy.tistory.com/36)

---

### 6. 요청 취소

요청의 수가 많은 SPA에선 요청 중에 사용자가 페이지를 전환하면 요청했던 것을 취소해주어야 합니다.

API 요청 취소는 간단합니다. `XHR`에서 제공하는 `abort` 메소드를 호출하는 것으로 취소시킬 수 있습니다. 또는 라이브러리에서 제공하는 메소드를 사용하면 됩니다.

axios에서는 `cancel token`을 이용해서 요청을 취소할 수 있습니다.

[Axios에서 요청 취소하는 방법](https://github.com/axios/axios#cancellation)

---

### 7. 동일 출처 정책 문제 해결

1. 서버측에서 CORS 설정
2. JSONP(JSON with Padding) 이용

   - 웹브라우저에서 css나 js 같은 리소스 파일들은 동일출처 정책에 영향을 받지 않고 로딩이 가능합니다. 이런 점을 응용하여 외부서버에서 js파일을 읽듯이 요청한 결과를 json으로 바꿔주는 편법적인 방법입니다. 단점은 리소스 파일을 `GET` 메소드로 읽어오기 때문에 `GET` 방식의 API만 요청이 가능합니다.

   - 또 JSONP를 이용한 방법은 서버측의 도움도 필요합니다.
   - [자세한 실행방법은 여기를 참고하세요-Jsonp 알고 쓰자](https://kingbbode.tistory.com/26)

3. CORS 요청 핸들링하기.

   - 모든 요청의 응답에 아래처럼 header를 추가하여 처리할 수 있다.

   ```js
   axios.get('https://a.4cdn.org/a/threads.json', {
     headers: {
       'Access-Control-Allow-Origin': '*',
     }
   }
   ```

## 2. fetch API

[fetch 스펙-영문](https://fetch.spec.whatwg.org/#concept-bodyinit-extract)

[FetchAPI와 XHR의 차이점이 모냐??](https://stackoverflow.com/questions/35549547/what-is-the-difference-between-the-fetch-api-and-xmlhttprequest)

```markdown
웹페이지 전체를 리로드하지 않고 일부분만을 리로드하고 비동기식으로 데이터를 불러와 작업하는 `XMLHttpRequest` 객체가 있습니다.

그 동안 우리는 WEB에서 어떤 리소스를 비동기로 요청하기 위해서는 XHR 객체를 사용했어야 했습니다.

IE가 판치던 그 때에는, IE에서 AJAX 요청을 보내기가 까다로워서 `jquery AJAX`나 `axios`, `superagent`같은 라이브러리를 사용했습니다.

하지만 XHR은 잘 디자인되어있는 API가 아니었습니다.

XHR의 부족한 부분을 보완하기 위해서 Fetch API를 도입하였고,
이는 HTTP 요청에 최적화 되어있고 상태도 잘 추상화 되어 있습니다.

또 Promise를 기반으로 되어있기 때문에 상태에 따른 로직을 추가하고 처리하는데에 최적화되어있습니다.

fetch와 XHR 둘 다 서버에 ajax 요청을 할 수 있습니다만,
fetch에는 XHR에서 사용할 수 없는 몇가지 추가 기능이 있습니다.
```

- ajax를 구현하는 여러가지 방법 중 최신 방법이 바로 `fetchAPI`

- fetch는 자바스크립트로 구현되기때문에(?) 따로 API 설치를 할 필요가 없다고 합니다.

- 비교적 최근에 도입되어 `IE` 및 구형 안드로이드 브라우저(4.x)는 지원하지 않습니다.

  - Chrome
  - FireFox
  - Safari 6.1+
  - Internet Explorer 10+

- `fetch()`는 `Promise`를 반환합니다.

> Axios는 XHR을 사용하는데, `Service Worker`등의 최신 기술이 XHR을 지원하지 않으므로 Service worker를 사용할 예정이라면 Fetch API를 사용해야 함

> create-react-app 에도 Service Worker가 있네요

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

### 2. fetchAPI의 기본 사용법

많이 찾아봤는데 예제들이 다들 promise를 쓰더라구요

그런김에 우리도 `Promise`로 `fetch`를 써봅시다.

#### Promise.....사용법..복습..

1. `Promise`생성자는 콜백을 인수로 받는다. 첫번째 인수로 `resolve` 가 들어오는데, 콜백 안에서 `resolve`를 호출하면 **`resolve`에 인수로 준 값이 곧 Promise 객체의 결과값이 된다.**

1. 두번째 인수로는 `reject`가 들어온다 => 비동기 작업에서 에러가 발생했을 때 호출하는 함수

1. `then` 메소드를 통해 콜백을 등록해서, 작업이 끝났을 때 결과값을 가지고 추가 작업을 할 수 있다.

```javascript
function delay(ms, value) {
  return new Promise((resolve, reject) => {
    setImeout(() => {
      resolve(value); //resolve에 인수로 준 값이 promise 객체의 결과값이 된다.
    }, ms);
  });
}

delay(1000, "hello")
  .then(str => {
    // 위의 반환값이 then의 인수(str)에 들어간다
    return delay(2000, str + "world"); // str에 위의 반환값('hello')가 들어간 상태로 다시 함수가 실행된다. 이때의 결과값('hello world')이 채워진 통이 반환되고
  })
  .then(str => {
    // 위에서 반환된 값이 then의 인수(str)에 들어간다
    console.log(str);
  });
```

#### Get

```js
fetch("https://jsonplaceholder.typicode.com/posts")
  .then(res => res.json())
  .then(json => console.log(json));
```

```js
async function logFetch(url) {
  try {
    const res = await fetch(url);
    console.log(await res);
    // console.log(await res.text())
  } catch (err) {
    console.log("fetch failed", err);
  }
}
```

fetch로 get 요청을 보내면 `Response`를 반환합니다. Response안에는...괴상한..것들이..들어있어요 알고싶지 않은것들..

`res.text()`, `res.json()` 모두 response 값의 데이터 부분을 빼오는 역할을 합니다.

`text()` : 응답 텍스트를 문자열로 표시

`json()` : 응답 텍스트의 결과를 산출한다.

text와 json둘다 mdn에 적혀있는데 정확히 무슨 차이인지 모르겠어요 이건 좀 더 알아봐야겠어요! => [여기에있네요 fetch 블로그](https://github.github.io/fetch/)

근데 둘 다 똑같이 작동하는디..?;;;;;;;큼큼

#### POST, PUT, PATCH

```js
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST", // 'PUT', 'PATCH'도 동일
  body: JSON.stringify({
    title: "foo",
    body: "bar",
    userId: 1
  }),
  headers: {
    "Content-type": "application/json; charset = UTF-8"
  }
})
  .then(response => response.json())
  .then(json => console.log(json));

// 반환 되는 값
/*
{
  id: 101,
  title: 'foo',
  body: 'bar',
  userId: 1
}
*/
```

#### DELETE

```js
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "DELETE"
});
```

> `post`,`put`, `patch`, `delete`가 성공적이면 서버는 200대의 성공이라는 응답을 줄 것입니다. 하지만 jsonplaceholder는 더미 데이터 사이트이기 때문에, 사이트에서는 확인할 수 없어용

#### Filtering

```js
fetch("https://jsonplaceholder.typicode.com/posts?userId=1")
  .then(response => response.json())
  .then(json => console.log(json));
```

###

작성중에 참고하던 링크
https://github.com/github/fetch

https://developer.mozilla.org/ko/docs/Web/API/Fetch_API/Fetch%EC%9D%98_%EC%82%AC%EC%9A%A9%EB%B2%95

https://github.com/typicode/jsonplaceholder#how-to

---

### 3. 한번 써볼까요

#### create-react-app

```
npm init react-app my-app
```

#### dummy data

```
https://jsonplaceholder.typicode.com/users
```

#### .json()

Response의 body에 있는 텍스트를 JSON으로 바꾸어줍니다.

---

### 4. 동일 출처 정책 해결

요청 객체의 `mode` 속성을 사용함으로써 CORS 설정을 해줄 수 있습니다.

`mode` 속성에 올 수 있는 값으로는 아래의 세가지가 있습니다.

- `same-origin` : 다른 오리진(origin)에 있는 자원을 요청하면 에러가 납니다. 요청이 항상 같은 오리진에서 일어나도록 보장하기 위해 이 mode를 사용할 수 있습니다.
- `no-cors`(디폴트) : CDN에서 스크립트를 불러오거나, 다른 도메인 서버에서 이미지를 불러오는 등, 웹 플랫폼이 기본적으로 하는 일을 나타냅니다. `HEAD`, `GET`, `POST` 이외의 명령을 금지합니다.
  > 어려워서 못알아듣겠는 추가 설명 :::: 둘째로, 만약 ServiceWorkers가 이런 요청(request) 을 가로채게 되면, ServiceWorkers 는 간단한 헤더(simple-header) 이외의 어떤 헤더 정보도 추가하거나 수정할 수 없습니다. 셋째로, JavaScript 는 결과로 전달되는 Response 객체의 어떤 속성에도 접근할 수 없습니다. 이렇게 함으로써 ServiceWorkers 는 웹의 의미성(semantics) 에 영향 주지 않음을 보장하면서, 도메인 사이에서의 데이터 유출에 의한 시큐리티와 프라이버시 문제를 방지합니다.
- `cors` : 다른 업체들이 제공하는 다양한 API들에 접근할때 필요한 크로스-오리진(cross-origin) 요청을 위해 주로 사용하게 될 mode입니다. `header`정보의 경우 제한된 일부 정보만 볼 수 있고, `body` 정보는 완전히 공개됩니다.

```js
fetch(url, { mode: "same-origin" })
  .then(res => console.log(res.json())
```

---

#### 참고 링크

[MDN-fetch API](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API)

[MDN-Using FetchAPI](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API/Fetch%EC%9D%98_%EC%82%AC%EC%9A%A9%EB%B2%95)

[fetch-polyfill](https://github.com/github/fetch)

[fetchAPI와 async-await](https://developers.google.com/web/fundamentals/primers/async-functions?hl=ko)

[fetchAPI-Medium](https://medium.com/@kkak10/javascript-fetch-api-e26bfeaad9b6)

---

## 2.5 요청 취소

SPA에선 요청 중에 사용자가 페이지를 전환하면 요청했던 것을 취소해주어야 한다.

API 요청 취소는 간단하다. `XHR`에서 제공하는 `abort` 메소드를 호출하는 것으로 취소시킬 수 있다. 또는 라이브러리에서 제공하는 메소드를 사용하면 된다.

하.지.만.

fetchAPI는 요청을 취소할 수 있는 기능을 제공하지 않는다.

[Axios에서 요청 취소하는 방법](https://github.com/axios/axios#cancellation)

## 3. Polyfill

개발자가 특정 기능이 지원되지 않는 브라우저를 위해 사용할 수 있는 코드 조각이나 플러그인을 말한다. 폴리필은 보통 HTML5 및 CSS3와 오래된 브라우저 사이의 간격을 메꾸는 역할을 담당한다.

#### 참고 링크

[Modernizr-HTML5 Cross Browser Polyfills : 개발되어있는 폴리필을 모아놓은 페이지](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills)
