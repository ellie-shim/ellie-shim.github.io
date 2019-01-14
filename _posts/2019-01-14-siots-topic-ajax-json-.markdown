---
layout: post
title: "2주차 topic - Ajax, JSON"
subtitle: "siots"
categories: siots
tags: topic
comments: true
---

# 2주차 TOPIC - Ajax와 JSON

## 1. XMLHttpRequest (XHR)

브라우저가 가지고있는 객체이고 이 객체를 사용해 서버와 상호작용을 할 수 있다.

IE는 ActiveX 컴포넌트로 XHR 객체를 지원

그 외 브라우저는 기본적으로 XHR 객체를 지원

페이지 전체의 데이터를 새로 받아오지 않고도 특정 URL로부터 데이터를 받아올 수 있다. 이를 이용해 웹페이지는 사용자를 방해하지 않고도 페이지의 일부분만을 업데이트할 수 있다. => `Ajax 프로그래밍에 주로 사용된다.`

> XHR의 이벤트 기반 모델은 요즘의 Promise기반과 generator 기반의 비동기 프로그래밍 방식과 잘 맞지 않는다.

> 이 개체의 인스턴스를 만들고 요청을 보내서 사용할 수 있다. => Q. 인스턴스를 만들려면?

---

## 2. Ajax (Asynchronous Javascript and Xml)

### 1. Ajax란 ?

Ajax는 자바스크립트의 라이브러리 중 하나이며 Asynchronous Javascript and Xml (비동기식 자바스크립트와 xml)의 약자이다.

XHR 객체를 이용해서 전체 페이지를 새로 고치지 않고도 페이지의 일부만을 위한 데이터를 로드하는 기법

**Javascript를 사용한 비동기 통신, 클라이언트와 서버간에 XML 데이터를 주고받는 기술** 이라고 할 수 있다.

이 때 서버와는 다음과 같은 다양한 형태의 데이터를 주고받을 수 있다.

- JSON
- XML
- HTML
- 텍스트 파일 등

> 비동기 방식 : 웹페이지를 리로드하지 않고 데이터를 불러오는 방식.
> 페이지 리로드의 경우 전체 리소스를 다시 불러와야 하는데, 모든 데이터를 재요청할 경우 불필요한 리소스 낭비가 발생하게 되지만
> 비동기 방식을 이용할 경우 필요한 부분만 불러와 사용할 수 있으므로 낭비가 적다는 장점이 있다.

> `ajax로 요청을 보내라` = `자바스크립트로 요청을 보내라`

### 2. Ajax로 요청 보내기

ajax를 이용해서 요청을 보내는 방법은 아주 다양하다.

그 중 자주 쓰이는 것은 `axios` 와 `fetchAPI`가 있다.

### 3. Ajax의 장단점

#### 장점

1. 웹페이지의 속도 향상
1. 서버의 처리가 완료 될 때까지 기다리지 않고 처리가 가능하다.
1. 서버에서 Data만 전송하면 되므로 전체적인 코딩의 양이 줄어든다.
1. 기존 웹에서는 불가능했던 다양한 UI를 가능하게 해준다.
1. 웹 페이지 전체를 다시 로딩하지 않고도 웹 페이지의 일부분만을 갱신할 수 있다.
1. 웹 페이지가 로드된 후에 서버로 데이터 요청을 보낼 수 있다.
1. 웹 페이지가 로드된 후에 서버로부터 데이터를 받을 수 있다.
1. 백그라운드 영역에서 서버로 데이터를 보낼 수 있다.

#### 단점

1. 히스토리 관리가 안된다.(보안에 좀 더 신경을 써야한다.)
1. 연속으로 데이터를 요청하면 서버 부하가 증가할 수 있다.
1. XHR을 통해 통신을 하는 경우 사용자에게 아무른 진행 정보가 주어지지 않는다 => 그래서 아직 요청이 완료되지 않았는데 사용자가 페이지를 떠나거나 오작동할 우려가 발생하게 된다.(로딩 인디케이터를 사용하자!)
1. 지원하는 Charset이 한정되어있다. (바이너리 데이터\* 를 보내거나 받을 수 없다.)
1. ★동일 출처 정책(SOP)\*으로 인해 다른 도메인과는 통신이 불가능하다(Cross-Domain 문제) => 그 페이지와 같은 서버에 있는 주소로만 ajax 요청을 할 수 있다.

> \* 바이너리 데이터(binary data) : 이진파일. 2진수 데이터만으로 이루어진 파일(.exe, .dll, .zip과 같은 압축파일, .mp3, .mpg, .jpg 등의 멀티미디어 파일)

> \* 동일 출처 정책(SOP, Same-Origin Policy)
> 웹어플리케이션 보안 모델에서 중요한 개념중 하나
> 해당 정책으로 인해 자바스크립트로 다른 웹페이지 접근 시 같은 출처의 페이지에만 접근 가능하다. 같은 출처라는 것은 protocol, host명, port가 같다는 것을 의미한다.

### 4. Ajax의 한계

ajax를 사용하면 여러 장점을 가지지만, ajax로도 다음과 같은 일들은 처리할 수 없다.

1. ajax는 클라이언트가 서버에 데이터를 요청하는 클라이언트 풀링 방식\* 을 사용하므로, 서버 푸시 방식의 실시간 서비스는 만들 수 없다.

> \* 클라이언트 풀링(client pooling) 방식 : 사용자가 직접 원하는 정보를 서버에게 요청하여 얻는 방식을 의미한다. 이에 반해 서버 푸시(server push) 방식이란 사용자가 요청하지 않아도 서버가 알아서 자동으로 특정 정보를 제공하는 것을 의미한다. 요즘 많이 사용되는 스마트폰에서 각종 앱이 보내는 푸시 알림이 서버푸시 방식의 대표적인 예이다.

### 5. Ajax의 동작 원리

![ajax를 이용한 웹 응용 프로그램의 동작 원리](http://tcpschool.com/lectures/img_ajax_ajax_application.png)

① : 사용자에 의한 요청 이벤트가 발생합니다.

② : 요청 이벤트가 발생하면 이벤트 핸들러에 의해 자바스크립트가 호출됩니다.

③ : 자바스크립트는 XMLHttpRequest 객체를 사용하여 서버로 요청을 보냅니다. 이때 웹 브라우저는 요청을 보내고 나서, 서버의 응답을 기다릴 필요 없이 다른 작업을 처리할 수 있습니다.

④ : 서버는 전달받은 XMLHttpRequest 객체를 가지고 Ajax 요청을 처리합니다.

⑤와 ⑥ : 서버는 처리한 결과를 HTML, XML 또는 JSON 형태의 데이터로 웹 브라우저에 전달합니다. 이때 전달되는 응답은 새로운 페이지를 전부 보내는 것이 아니라 필요한 데이터만을 전달합니다.

⑦ : 서버로부터 전달받은 데이터를 가지고 웹 페이지의 일부분만을 갱신하는 자바스크립트를 호출합니다.

⑧ : 결과적으로 웹 페이지의 일부분만이 다시 로딩되어 표시됩니다.

![기존 웹 응용 프로그램의 동작 원리](http://tcpschool.com/lectures/img_ajax_other_application.png)

#### 참고링크

[Ajax란 무엇인가?](https://coding-factory.tistory.com/143)

[TCPSchool-Ajax](http://tcpschool.com/ajax/intro)

---

## 3. HTTP request methods

기억해야 할 메소드 **CRUD** : Create, Read, Update, Delete

#### Create

새로운 자료를 등록하는 작업

- ★`POST` : 서버에 새로운 데이터를 등록. (게시물 등록)

#### Read

자료의 본문을 요청하는 작업

- ★`GET` : 서버에 데이터 요청. 데이터를 받기만 한다. (게시물 읽기)

#### Update

자료의 본문을 수정하는 작업

- ★`PUT` : 서버의 데이터를 교체할 때. (게시물 수정)
- ★`PATCH` : 리소스의 부분만을 수정하는 데 쓰인다.

#### Delete

자료를 삭제하는 작업

- ★`DELETE` : 데이터 삭제

#### 그 외 메소드

- `HEAD` : `GET` 메소드의 요청과 동일한 응답을 요구하지만, 응답 본문을 포함하지 않는다.
- `CONNECT` : 목적 리소스로 식별되는 서버로의 터널을 맺는다.
- `OPTIONS` : 목적 리소스의 통신을 설정하는 데 쓰인다.
- `TRACE` : 목적 리소스의 경로를 따라 메시지 loop-back 테스트를 한다.

#### 참고 링크

[HTTP 요청 메소드](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods)

---

## 4. Response Status

### 1. Status Category

**2xx** : 성공

**3xx** : 추가 작업이 필요함

**4xx** : 실패- 클라이언트 책임

**5xx** : 실패 - 서버 책임

### 2. Status Code

#### 2xx

**200 OK** : 성공

**201 Created** : 자료가 성공적으로 생성됨

#### 3xx

**301 Moved Permanently(Redirection)** : 자료가 완전히 다른 곳으로 이동했음

**302 Fount(Redirection)** : 자료가 일시적으로 다른 곳에 있음

**304 Not Modified (cache)** : 클라이언트가 이미 가지고 있던 자료가 수정되지 않았음(그대로 사용하면 됨)

#### 4xx

**400 Bad Request** : 요청의 형태가 잘못되어 응답할 수 없음

**403 Forbidden** : 요청한 자료에 접근할 권한이 없음

**404 Not Found** : 요청한 자료가 없음

#### 5xx

**500 Internal Server Error** : 요청을 처리하던 중에 예상치 못한 오류가 발생함

**503 service Unavailable** : 서버가 일시적으로 응답을 할 수 없음

#### 참고 링크

[HTTP Status Codes](https://httpstatuses.com/)

### 3. Header

요청과 응답에 대한 추가 정보를 표현하는데 사용 됨

인증, 캐싱, 쿠키, 보안, 프록시 등 웹 표준에 정의된 많은 기능을 제어하는데 사용 됨.

#### Authorization

요청의 인증 정보

#### User-Agent

요청 중인 클라이언트의 정보

#### Location

301, 302 응답에서 자료의 위치

#### Accept

요청이 어떤 형태의 자료를 원하는지 나타냄

#### Content-Type

요청 혹은 응답이 어떤 형태의 자료인지 나타냄

---

## 5. JSON

### 1. JSON ?

JavaScript Object Notation의 약자이다.

JSON은 언어가 아니라 **데이터 형식**이다.

프로그래밍 언어에서 **파싱**과 **직렬화**를 지원한다.

### 2. 다룰 수 있는 데이터형

- false
- true
- null
- object
- array
- 수치
- string

### 3. 사용 방식

키와 값으로 데이터를 가지고 있는 딕셔너리(Dictionary)
데이터를 배열로 들고있는 리스트(List)

두가지 방식으로 사용 가능하며 두가지를 자유롭게 조합하여 사용할 수도 있다.

- Dictionary

  ```JSON
  {
    'studyname' : 'siots',
    'location' : 'studybloom',
    'person' : 4
  }
  ```

- List

  ```JSON
  ['html', 'css', 'javascript', 'react']
  ```

- Dictionary + List
  ```JSON
  [
    {
      'username' : 'henry',
      'age' : 28
    } ,
    {
      'username' : 'domino',
      'age' : 21
    }
  ]
  ```

### 4. 장점

JSON 데이터는 단순하고 가볍게, 문자열을 Javascript에서 간단하게 읽어올 수 있다는 점에서 Ajax에서 JSON을 널리 이용하게 되었다.

다양한 오브젝트를 전송하거나 할 때 오브젝트를 문자열로 간단하게 변환하여 보낼 수 있다는 장점이 있다.

### 5. JSON은 세가지 타입을 사용한다.

- 단순한 값 : 문자열, 숫자, boolean, null은 해당되지만 `undefined`는 지원되지 않는다.
- 객체 : 순서가 있는 key-value 쌍이다.
- 배열 : 인덱스로 접근할 수 있는 순서있는 목록이다.

### 3. 파싱과 직렬화

#### stringify(), 직렬화

- javascript 객체를 JSON 문자열로 직렬화
- JSON 문자열에 공백 & 들여쓰기가 없으며 함수, 프로토타입 멤버, 값이 `undefined`인 프로퍼티가 생략된다.

```js
const book = {
  title: "bookname",
  authors: ["Kendrick"],
  edition: 3,
  year: 2011
};

const jsonText = JSON.stringify(book);
console.log(jsonText);
//console:{"title":"bookname","authors":["Kendrick"],"edition":3,"year":2011}
```

#### 직렬화 옵션

- `stringify()` 메소드에 매개변수를 추가할 수 있다.
- 추가 매개변수 1 : **필터(replacer)**에 해당되며 배열, 함수를 사용할 수 있다. (해당 key 값만 JSON 문자열로 직렬화 한다.)
- 추가 매개변수 2 : JSON 문자열 들여쓰기를 조절한다.

```js
const album = {
  title: "X",
  release: 2019,
  songs: ["sing", "sang", "song"]
};

// 추가 매개변수 1 : 해당 key 값만 직렬화 한다.
const jsonText = JSON.stringify(album, ["title", "release"]);

console.log(jsontext); // {"title":"X", "release" : 2019}

// 추가 매개변수 1 : 함수
const jsonTextFunc = JSON.stringify(album, function(key, value) {
  switch (key) {
    case "songs":
      return value.join("-");
    default:
      return value;
  }
});

console.log(jsonTextFunc); //{"title":"X","release":2019,"songs":"Sing-Sang-Song"}

//추가 매개변수 2 : 들여쓰기
const jsonTextTab = JSON.stringify(album, null, 8);
console.log(jsonTextTab); // 8칸 들여쓰기 된 객체가 출력된다.
```

#### 직렬화 심화

- 객체에 `toJSON()` 메소드를 추가할 수 있다.(예 : `new Date().toJSON()` )

- `toJSON()` 메소드가 있을 경우 호출하여 리턴된 값을 사용하고 없을 경우 기본 직렬화 방법을 사용한다.
- 필터 함수에 전달되는 값은 `toJSON` 메소드에서 반환된 값에 해당된다.

```js
const album = {
  title: "X",
  release: 2019,
  songs: ["Sing", "Sang", "Song"],
  toJSON: function() {
    return this.songs.join("-");
  }
};

var jsonText = JSON.stringify(album);

console.log(jsonText); // 'Sing-Sang-Song'
```

=> 잘 모르겠음..

#### parse(), 파싱

- JSON을 파싱하여 네이티브 자바스크립트 값으로 변환한다.
- 직렬화 되기 전 자바스크립트 객체와 파싱 된 객체는 동일하지 않다.

#### 파싱 옵션

- parse()메소드에 매개변수를 추가할 수 있다.
- `stringify()`에서 사용하는 **필터** 함수와 형식은 같으나 구분을 위해 **리바이버(reviver)** 함수라 부른다
- 매개변수로 key-value 값을 받으며 반환 값도 있다.

---

## 면접 문제

1. Ajax란 무엇인가 ?
1. Ajax를 사용하면 문제가 있다. 그 문제는 무엇인가?
1. (심화) 그 문제를 해결하려면 어떻게 해야하는가?
