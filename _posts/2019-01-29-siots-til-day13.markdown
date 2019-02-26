---
layout: post
title: "13일차 - 시멘틱마크업"
subtitle: "siotz"
categories: siotz
tags: til
comments: true
---

# 추후에 정리가 필요한 문서입니다!!!

# 13일차

# 1. 시멘틱 마크업

HTML5부터 시멘틱 태그가 추가되어, 시멘틱 마크업을 하기로했다.

HTML5로 만든 웹페이지를 시멘틱웹이라고도 한다.

#### 시멘틱 태그의 기본적인 구성

![구성](https://t1.daumcdn.net/cfile/tistory/261CDE33564B2D3D2E)

#### 시멘틱 구조 태그

- header
- nav
- aside
  - 본문이랑 동떨어진 내용 광고 배너같은 부분
  - 본문과 분리된 작은 내용
- section

  - 관심사 그룹에 따라 구문하기 위해 사용
  - 반드시 제목요소(h1~h6)를 가져야한다.

- article
  - 관심사에 따라 글을 작성하는 요소
  - article로 감싼 부분은 반드시 독립적으로 존재해도 되는 경우여야한다
  - 반드시 제목요소(h1~h6)를 가져야한다.
  - `section`안에 `article`이 있어도 되고 `article`안에 `section`이 있어도 된다.

> article은 독립적! section은 그룹!

- footer
  - 주소나 저작권, 연락처
  - 일반적으로 footer는 문서 내 한번만 사용되지만, section이나 article같은 작은 영역 안에서도 사용할 수 있다.
- main : 해당 페이지의 main콘텐츠. 한 페이지당 한번만 사용 가능.
- h1~h6
  - `h1` : 컨텐츠의 메인 타이틀
  - `h2` : section의 헤더라인
  - `h3` : 서브섹션의 헤드
  - 위와 같은 방식으로 사용할 수 있다.

#### `시멘틱 웹페이지`를 구현하는 이유

[Poiemaweb-시멘틱 요소와 검색 엔진](https://poiemaweb.com/html5-semantic-web)

# 2. CSS 방법론

## 1. BEM(Block Element Modifier)

class의 이름을 짓는데 구조적인 방법을 제시한다.

BEM방법론은 `#id`에는 적용할 수 없고 `.class` 명에만 적용한다.

BEM은 개발, 디버깅, 유지보수를 위하여 CSS 선택자의 이름을 가능한 한 명확하게 만드는 것이 목표이다.

최대한 간결하지만 의미를 담고있는게 핵심이다.

#### 작명 규칙

소문자, 숫자 만을 이용해서 작명한다

여러 단어의 조합은 하이픈(-)으로 연결하여 작명한다.

#### Block

- block은 문단 전체에 적용된 element 또는 element를 담고 있는 컨테이너를 말한다.
- 재사용할 수 있고 기능적으로 독립적인 페이지 구성 요소
- 형태(red, big, ...)가 아닌 목적(menu, button, ...)에 맞게 결정해야 한다.
- 블록은 환경에 영향을 받지 않아야 한다. 즉, 여백이나 위치를 설정하면 안된다.
- 블록은 서로 중첩해서 작성 할 수 있다.
- 형태

#### Element

- block안에서 특정 기능을 수행하는 컴포넌트
- element는 상황에 따라 달라진다

[BEM 퀵스타트](https://en.bem.info/methodology/quick-start/)

## 2. OOCSS(Object Oriented CSS)

- 객체 지향 CSS
- CSS를 모듈 방식으로 코딩하여 중복을 최소화하는 기법
- 두가지 원칙에 기초해있다

#### 첫번째 원칙, 겉모양(skin)에서 골격(structure)을 분리하기

구조와 외양을 분리하자. 외양(skin)으로 분리시켜, 결합시키면 다양한 결과물을 얻을 수 있음.

이렇게 하면, 모든 요소들은 클래스를 두 개 이상 사용하게 된다.
하지만 공통 스타일과 재사용 가능한 "겉모양"용 스타일을 결합해 사용하면서 불필요한 반복은 없어진다.
더군다나 코드는 줄었고, 재사용의 가능성이 늘었다.

#### 두번째 원칙, 컨테이너와 콘텐츠를 분리하기

다른 영역에서도 사용가능하도록 .header-inside라는 속성으로 추출(분리)하면,
중복 코드를 사용하게 되는 경우가 적어진다.

### 클래스 네이밍 방법

- 가능한 짧고 간결하게 작성한다.
- 동작과 형태가 예상 가능하도록 명확하게 작성한다.
- 어떻게 생겼는지 보다는 어떤 목적인지 알 수 있도록 의미있게 작성한다.
- 지나치게 구체적이지 않게 일반적으로 사용가능 하도록 작성

### OOCSS의 장점

- 많은 CSS 코드가 재사용되면서 코드의 길이가 줄어든다. 즉 css 파일 크기가 작아져서 속도를 향상 시킬 수 있다.
- 새로운 요소를 추가할때, 기존 모듈을 통해서 재사용이 가능하고 쉽게 확장 가능하여 유지보수성이 높아진다.

### OOCSS의 단점
- 복잡해지는 HTML이 오히려 유지보수를 어렵게 하고 가독성을 떨어뜨려 비판적인 시선이 많다.
- Sass와 함께 사용하게 되면 단점을 보완할 수 있음
- Sass의 mixin, extend 방식을 사용하면 Semantic한 HTML코드를 얻을 수 있다.(extend 방식이 컴파일시 코드중복이 적어서 extend사용이 더 좋다.)

#### mixin 방식
```css
@mixin btnbase {
	border: 3px solid #000;
	padding: 10px 20px;
	color: #fff;
	border-radius: 10px;
}

.twitterbtn {
	@include btnbase;
	background: red;
}
.facebookbtn {
	@include btnbase;
	background: gray;
}
```

#### extend 방식
```css
.btnbase {
	border: 3px solid #000;
	padding: 10px 20px;
	color: #fff;
	border-radius: 10px;
}

.twitterbtn {
	@extend .btnbase;
	background: red;
}
.facebookbtn {
	@extend .btnbase;
	background: gray;
}
```

## 3. SMACSS (Scalable and Modular Architecture for CSS)

- 대규모 프로젝트를 위한 스타일링 지침
- 스타일을 다섯가지로 분류하고 각 유형에 맞는 선택자와 작명법, 코딩 기법을 제시한다.

# 3. Flex
- flexbox는 뷰포트나 요소의 크기가 불명확하거나 동적으로 변할 때에도 효율적으로 요소를 배치, 정렬, 분산할 수 있는 방법을 제공하는 CSS3의 새로운 레이아웃 방식
- 1차원 레이아웃 대상

[코드펜-flex](https://codepen.io/Shim-SoYoung/pen/gqwbrx)

# 4. Grid


- 2차원 레이아웃