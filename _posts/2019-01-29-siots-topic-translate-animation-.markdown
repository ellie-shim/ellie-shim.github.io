---
layout: post
title: "4주차- CSS - translate, animation"
subtitle: "siots"
categories: siots
tags: topic
comments: true
---

# 4주차 topic 2 - CSS - translate, animation

# translate

# Animation

## @keyframes

애니메이션에서 가장 중요한 부분은 `@keyframes`입니다.
@keyframes은 애니메이션이 만들어지는 부분입니다. 타임라인 안의 하나이 스테이지(구간)들이라고 생각하세요.

`@keyframes`안에서 스테이지들을 정의하고 각 구간마다 다른 스타일을 적용 시킬 수 있습니다.

#### 속성

- 내가 정하는 이름
- 스테이지 : 0% - 100% 또는 from(0%와 같음) - to(100%와 같음)
- 각 구간에 적용시킬 CSS 스타일

```css
@keyframes siots {
  /* 0% 또는 from */
  0% {
    opacity: 1;
  }
  /* 100% 또는 to */
  100% {
    opacity: 0;
  }
}
```

## Animation

애니메이션은 여러개의 속성을 가질 수 있습니다.

- `animation-name` : `@keyframes` 이름 (위에서는 siots
  )
- `animation-duration` : 타임 프레임 길이. 애니메이션 시작부터 마지막까지의 총 지속시간
- `animation-timing-function` : 애니메이션 속도 조절
  - linear
  - ease
  - ease-in : 느리게-빠르게
  - ease-out : 빠르게-느리게
  - ease-in-out : 느리게-빠르게-느리게
  - cubic-bezier
- `animation-delay` : 애니메이션이 시작하기 전 지연시간
- `animation-iteration-count` : 반복 횟수
- `animation-direction` : 루프 방향. 정방향으로 반복, 역박향으로 반복, 번갈아가며 반복 등을 설정
- `animation-fill-mode` : 애니메이션 시작/끝 상태 제어
  - none
  - forwards
  - backwards
  - both

## 단축 표기법

- 선언 순서는 상관없다
- 값과 값 상태를 띄어쓰기로 구분
- `animation-name`, `animation-duration`은 필수값
- duration 1s, delay 1s로 둘다 똑같을때, duration은 필수값이기 때문에 먼저 선언된 (n)s를 duration으로 인식한다.

## 여러개의 애니메이션 적용

복수의 애니메이션을 추가하려면 **쉼표**를 사용해서 분리할 수 있습니다.
`@keyframes`을 여러개 선언하고 엘리먼트에 쉼표를 사용하여 묶어줍니다

```css
@keyframes siots {
  /* style */
}
@keyframes yoonho {
  /* style */
}
.element {
  animation: siots 4s 1s infinite linear alternate, yoonho 4s 1s infinite linear
      alternate;
}
```

## Vendor Prefixes 더하기

작업을 하면서 브라우저에 맞는 프리픽스를 사용하여 브라우저 지원이 가능한 잘 되도록 합니다.

- 크롬 & 사파리 : `-webkit-`
- 파이어폭스 : `-moz-`
- 오페라 : `-o-`
- 인터넷 익스플로러 : `-ms-`

#### 사용 방법

animation

```css
.element {
  -webkit-animation: siots 4s 1s infinite linear alternate;
  -moz-animation: siots 4s 1s infinite linear alternate;
  -ms-animation: siots 4s 1s infinite linear alternate;
  -o-animation: siots 4s 1s infinite linear alternate;
  animation: siots 4s 1s infinite linear alternate;
}
```

@keyframes

```css
@-webkit-keyframes siots {
  /* your style */
}
@-moz-keyframes siots {
  /* your style */
}
@-ms-keyframes siots {
  /* your style */
}
@-o-keyframes siots {
  /* your style */
}
@keyframes siots {
  /* your style */
}
```

#### 파이어폭스에서의 애니메이션

파이어폭스에서는 변형하는 오브젝트가 이상하게 렌더링 됩니다. 해당 요소(element)에 투명한 외곽선을 추가하면 파이어폭스에서도 이쁘게 랜더해줍니다

```css
.element {
  /* ~animation style~ */
  outline: 1px solid transparent;
}
```

## 지원 브라우저

[자세한 버전별 지원은 CanIUse를 참고하세요!](https://caniuse.com/#feat=css-animation)

- Firefox 5+
- IE 10+
- Chrome
- Safari 4+
- Opera 12+

## 실습하러 가봅시다

[실습용 codepen- fork해주세요!](https://codepen.io/Shim-SoYoung/pen/Norrxj)

[튜토리얼 강좌 링크 - 스크롤 40%](https://webdesign.tutsplus.com/ko/tutorials/a-beginners-introduction-to-css-animation--cms-21068)

#### 참고 링크

[css3please](http://css3please.com/)

[animation-timing-function 예제들](https://matthewlein.com/tools/ceaser)
