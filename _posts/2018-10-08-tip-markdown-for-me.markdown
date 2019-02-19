---
layout: post
title: "나를 위한 마크다운 문법"
subtitle: "markdown"
categories: tip
tags: tip
comments: true
---

# 나를 위한 마크다운 문법

```xml
# 1번 제목
## 2번 제목
### 3번 제목
#### 4번 제목
```

# 1번 제목

## 2번 제목

### 3번 제목

#### 4번 제목

---

```xml
> 인용문
>
> > 인용 안의 인용
> > # 인용 안의 제목
```

> 인용문
>
> > 인용 안의 인용
> >
> > ## 인용 안의 제목

---

```xml
* 순서가 없는
+ 목록
- 섞어서도 쓸수있다
  + tab키 또는
  + 띄어쓰기 두칸으로
  + Depth
    * 가능
```

- 순서가 없는

* 목록

- 섞어서도 쓸수있다
  - tab키 또는
  - 띄어쓰기 두칸으로
  - Depth
    - 가능

---

```xml
1. 순서가 있는
1. 목록
1. 알아서 카운팅
  1. 마찬가지로
  1. Depth
```

1. 순서가 있는
1. 목록
1. 알아서 카운팅
1. 마찬가지로
1. Depth

---

```xml
강조 문법 *기울기*
두가지 _방법_
```

강조 문법 _기울기_
두가지 _방법_

---

```xml
강조 문법 **굵게**
두가지 __방법의 볼드__
```

강조 문법 **굵게**
두가지 **방법의 볼드**

---

```xml
[링크도 가능](https://ellie-shim.github.io)
```

[링크도 가능](https://ellie-shim.github.io)

---

```xml
느낌표를 붙여주면 이미지 삽입도 가능
![비비](https://ellie-shim.github.io/assets/img/bb-pic.png)
```

![비비](https://ellie-shim.github.io/assets/img/bb-pic.png)

---

````xml
\``` 백틱이나
\~~~ 물결로 시작할 수 있다.
중요한 코드블럭
\```javascript
옆에 키워드를 입력하면 해당 코드의 구문 강조 스타일이 들어감.
````

- javascript
- css
- html => xml
- markdown

### 코드블럭 구문강조 지원언어 참고

[구문 강조를 위한 펜스 코드 블럭(fenced code block)](http://haroopress.com/post/fenced-code-block/)
