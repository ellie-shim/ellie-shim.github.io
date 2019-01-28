---
layout: post
title: "4주차- CSS - transition, animation"
subtitle: "siots"
categories: siots
tags: topic
comments: true
---

# 4주차 topic 2 - CSS - transition, animation

# transform (변형)

CSS3에서는 `transform` 속성을 사용하여 요소의 스타일을 자유롭게 바꿀 수 있습니다.

- 해당 요소를 움직입니다
- 해당 요소를 회전시킵니다
- 해당 요소의 크기를 변경합니다
- 해당 요소를 기울입니다
- 해당 요소에 위의 네가지 동작 중 원하는 동작들을 한 번에 적용시킵니다.

`transform`에서는 `x`, `y`, `z` 좌표를 사용하고 기준점은 **브라우저의 왼쪽 상단**이 됩니다.

- `x`축 : 오른쪽이 양(+)의 방향
- `y`축 : 아래쪽이 양(+)의 방향
- `z`축 : 모니터를 바라보고있는 내 쪽이 양(+)의 방향,(반대가 음(-)의 방향)

## 2D transform

### 지원 브라우저

<table class="tb-1" summary="">
	<tbody>
		<tr>
			<th>속성</th>
			<th><img alt="ie" class="icon" src="/img/icon-ie.png"></th>
			<th><img alt="chrome" class="icon" src="/img/icon-chrome.png"></th>
			<th><img alt="firefox" class="icon" src="/img/icon-firefox.png"></th>
			<th><img alt="safari" class="icon" src="/img/icon-safari.png"></th>
			<th><img alt="opera" class="icon" src="/img/icon-opera.png"></th>
		</tr>
		<tr>
			<td>
			<p>transform</p>
			<p>transform-origin</p>
			</td>
			<td>
			<p>10.0</p>
			<p>9.0 -ms-</p>
			</td>
			<td>
			<p>36.0</p>
			<p>4.0 -webkit-</p>
			</td>
			<td>
			<p>16.0</p>
			<p>3.5 -moz-</p>
			</td>
			<td>
			<p>9.0</p>
			<p>3.2 -webkit-</p>
			</td>
			<td>
			<p>23.0</p>
			<p>15.0 -webkit</p>
			<p>12.1</p>
			<p>10.5 -o-</p>
			</td>
		</tr>
	</tbody>
</table>
# translate (전환)

CSS 속성을 변경할 때, 변경이 즉시 영향을 미치게 하는 대신 그 **속성의 변화가 일정 기간에 걸쳐 일어나도록** 할 수 있습니다.

`transition`은 1단계적인 전환만 가능합니다. `border-radius`를 여러 단계에 걸쳐서 전환하는 것은 불가능합니다.(animation으로 가능)

> `.appendChild()`로 DOM에 요소를 추가하거나 `display:none` 속성을 제거하고 나서 바로 transition을 사용할 때 주의해야합니다. 초기상태가 진행되지않고 마지막 변경이 완료된 결과만 확인될 수도 있습니다. `window.setTimeout()`을 이용해 속성 변경 전에 밀리초를 주어 해결할 수 있습니다.

## 속성

- `transition`
  - 단축 표기법으로 아래의 속성들을 한 줄에 정의할 수 있음
- `transition-delay`
  - 전환 효과가 나타나기 전까지의 지연 시간
- `transition-duration`
  - transition이 일어나는 지속 시간을 명시합니다.
- `transition-property`

  - transition을 적용해야 하는 CSS속성의 이름을 명시합니다. 여기에 나열 된 속성들만 transition하는 동안 움직입니다.
  - 나열되지않은 속성의 변화는 보통 때와 같이 즉시 일어납니다.
  - `all`이라는 값을 주면 적용되는 모든 변화가 선택됩니다.

- `transition-timing-function`
  - transition의 속도를 조절합니다
  - ease : **기본값**, 전환효과가 천천히 시작되어, 빨라지고, 마지막엔 다시 느려짐
  - linear : 일정한 속도로 진행
  - ease-in : 전환효과가 느리게 시작함
  - ease-out : 전환효과가 천천히 끝남
  - cubic-bezier(n,n,n,n) : 사용자가 정의한 함수에 따라 진행 됨
  - step-end : 전환이 과정 없이 지정한 `duration`시간 뒤에 바로 전환됨
  - steps(n, end) : 전환효과가 지정한 `duration` 시간 동안 n번의 스텝으로 진행 됨

## 사용법

전환하기 전 기본 상태를 스타일링하고 액션이 일어났을 때(`:hover`나 클릭 이벤트) 변환 될 스타일링을 설정해 줍니다.

```css
.box {
  /* 기본 style */
}
.box:hover {
  /* 마우스 오버시 전환 될 스타일 */
}
```

그리고 기존 `.box`에 `transition` 효과를 설정해 줍니다.

```css
.box{
  /* 기본 스타일 */
  transition : width 2s, height 2s, background-color : 2s;
  /* 또는 all로 모든 속성을 선택할 수 있습니다 */
  transition : all 2s
}
```

[transition 예제](https://codepen.io/Shim-SoYoung/pen/OdXgVN)

## 지원 브라우저

[자세한 버전별 지원은 CanIUse를 참고하세요!](https://caniuse.com/#feat=css-transitions)

<table class="tb-1" summary="">
	<tbody>
		<tr>
			<th style="width: 25%;">속성</th>
			<th><img alt="ie" class="icon" src="/img/icon-ie.png"></th>
			<th><img alt="chrome" class="icon" src="/img/icon-chrome.png"></th>
			<th><img alt="firefox" class="icon" src="/img/icon-firefox.png"></th>
			<th><img alt="safari" class="icon" src="/img/icon-safari.png"></th>
			<th><img alt="opera" class="icon" src="/img/icon-opera.png"></th>
		</tr>
		<tr>
			<td>
			<p>transition</p>
			<p>transition-delay</p>
			<p>transition-duration</p>
			<p>transition-property</p>
			<p>transition-timing-function</p>
			</td>
			<td>
			<p>10.0</p>
			</td>
			<td>
			<p>26.0</p>
			<p>4.0 -webkit-</p>
			</td>
			<td>
			<p>16.0</p>
			<p>4.0&nbsp;-moz-</p>
			</td>
			<td>
			<p>6.1</p>
			<p>3.1 -webkit-</p>
			</td>
			<td>
			<p>12.1</p>
			<p>10.5&nbsp;-webkit</p>
			</td>
		</tr>
	</tbody>
</table>

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

<table class="tb-1" summary="">
	<tbody>
		<tr>
			<th style="width: 25%;">속성</th>
			<th><img alt="ie" class="icon" src="/img/icon-ie.png"></th>
			<th><img alt="chrome" class="icon" src="/img/icon-chrome.png"></th>
			<th><img alt="firefox" class="icon" src="/img/icon-firefox.png"></th>
			<th><img alt="safari" class="icon" src="/img/icon-safari.png"></th>
			<th><img alt="opera" class="icon" src="/img/icon-opera.png"></th>
		</tr>
		<tr>
			<td>
			<p>@keyframes</p>
			<p>animation</p>
			</td>
			<td>
			<p>10.0</p>
			</td>
			<td>
			<p>43.0</p>
			<p>4.0 -webkit-</p>
			</td>
			<td>
			<p>16.0</p>
			<p>5.0&nbsp;-moz-</p>
			</td>
			<td>
			<p>9.0</p>
			<p>4.0&nbsp;-webkit-</p>
			</td>
			<td>
			<p>30.0</p>
			<p>15.0&nbsp;-webkit</p>
			<p>12.0 -o-</p>
			</td>
		</tr>
	</tbody>
</table>

## 실습하러 가봅시다

[실습용 codepen- fork해주세요!](https://codepen.io/Shim-SoYoung/pen/Norrxj)

[튜토리얼 강좌 링크 - 스크롤 40%](https://webdesign.tutsplus.com/ko/tutorials/a-beginners-introduction-to-css-animation--cms-21068)

### 버튼을 누르면 돌아가게 해봅시다

1. html에 버튼을 class명을 지정해 생성해줍니다
1. 버튼 스타일을 지정해줍니다
1. `div`에 지정해준 animation 속성을 class를 생성해 따로 빼줍니다.
1. 버튼과 애니메이션을 줄 `div`를 선택해 변수에 담아줍니다
1. 버튼에 이벤트리스너를 걸어줍니다.

#### 참고 링크

[css3please](http://css3please.com/)

[animation-timing-function 예제들](https://matthewlein.com/tools/ceaser)
