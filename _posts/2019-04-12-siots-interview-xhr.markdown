---
layout: post
title: "면접질문 정리해보기 5 - XHR"
subtitle: "siotz"
categories: siotz
tags: interview
comments: true
---

1. XHR ?

- ajax 요청을 보내는 객체.

1. XHR 요청 보내는 방법 코딩해보기

   1. XHR 객체 생성 후 GET : 쿼리스트링으로 요청 가능

   ```js
   const xhr = new XMLHttpRequest(); // 생성자 함수로 XHR 인스턴스 생성
   xhr.onload = function() {
     // 요청을 보내고
     if (xhr.status === 200 || xhr.status === 201) {
       // 요청에 성공하면
       console.log(xhr.responseText); // 응답 객체의 responseText를 불러와라. => 여기에 데이터가 담겨있음
     } else {
       // 오류가 나면
       console.error(xhr.responseText); // 에러의 응답객체
     }
   };
   xhr.open("GET", "https://broad-chauffeur.glitch.me/products?id=1"); // 여기로 get 요청할거고
   xhr.send(); // 이제 요청을 보내라!
   ```

   1. POST 요청 - 1

   ```js
   const xhr = new XMLHttpRequest();
   const data = {
     title: "naver tech",
     body: "it was a useful time. it was very interesting"
   };
   xhr.onload = function() {
     // 요청을 보내고
     if (xhr.status === 200 || xhr.status === 201) {
       // 요청에 성공하면
       console.log(xhr.responseText); // 응답 객체의 responseText를 불러와라. => 여기에 데이터가 담겨있음
     } else {
       // 오류가 나면
       console.error(xhr.responseText); // 에러의 응답객체
     }
   };
   xhr.open("POST", "https://jsonplaceholder.typicode.com/posts"); // 이 주소로 post를 보낼거다
   xhr.setRequestHeader("Content-Type", "application/json"); // 콘텐트 타입은 json으로
   xhr.send(JSON.stringify(data)); // data 를 직렬화해서 보낸다.
   ```

   1. POST 요청 - 2

   ```js
   const xhr = new XMLHttpRequest();
   const formData = new FormData();
   formData.append("title", "naver tech");
   formData.append("body", "it was a useful time. it was very interesting");

   xhr.onload = function() {
     // 요청을 보내고
     if (xhr.status === 200 || xhr.status === 201) {
       // 요청에 성공하면
       console.log(xhr.responseText); // 응답 객체의 responseText를 불러와라. => 여기에 데이터가 담겨있음
     } else {
       // 오류가 나면
       console.error(xhr.responseText); // 에러의 응답객체
     }
   };
   xhr.open("POST", "https://jsonplaceholder.typicode.com/posts"); // 이 주소로 post를 보낼거다
   xhr.senad(formData);
   ```

> 더미사이트에 post 할 때 1번의 객체 형식의 데이터를 JSON 타입으로 stringify하고 보내면 응답 객체로 포스트한것+아이디 이렇게 잘 들어오는데, 2번의 formData 인스턴스에 append 해서 보내는건 응답객체에 아이디값만 돌아온다 왜일까!?!?

> 파싱 : JSON 형태의 데이터를 우리가 사용할 수 있는 객체로 변환하는것!
