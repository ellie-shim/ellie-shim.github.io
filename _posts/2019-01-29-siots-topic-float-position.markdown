---
layout: post
title: "4주차- CSS - float, position"
subtitle: "siots"
categories: siots
tags: topic
comments: true
---

# 4주차 topic 1 - CSS - float, position

# float

CSS 속성(property) `float`은 한 요소(element)가 보통 흐름(normal flow)으로부터 빠져 텍스트 및 인라인(inline) 요소가 그 주위를 감싸는 자기 컨테이너의 좌우측을 따라 배치되어야 함을 지정합니다 _갑분영어공부_

```markdown
defalt : `none`
적용대상 : `display` 가 `none`이 아닌 모든 요소

상속 : NO
```

`float`은 블록 레이아웃의 사용을 뜻하기 때문에, 일부 경우에 `display` 값의 계산값을 수정합니다.

<table class="standard-table">
 <thead>
  <tr>
   <th scope="col">지정값(Specified value)</th>
   <th scope="col">계산값</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>inline</code></td>
   <td><code>block</code></td>
  </tr>
  <tr>
   <td><code>inline-block</code></td>
   <td><code>block</code></td>
  </tr>
  <tr>
   <td><code>inline-table</code></td>
   <td><code>table</code></td>
  </tr>
  <tr>
   <td><code>table-row</code></td>
   <td><code>block</code></td>
  </tr>
  <tr>
   <td><code>table-row-group</code></td>
   <td><code>block</code></td>
  </tr>
  <tr>
   <td><code>table-column</code></td>
   <td><code>block</code></td>
  </tr>
  <tr>
   <td><code>table-column-group</code></td>
   <td><code>block</code></td>
  </tr>
  <tr>
   <td><code>table-cell</code></td>
   <td><code>block</code></td>
  </tr>
  <tr>
   <td><code>table-caption</code></td>
   <td><code>block</code></td>
  </tr>
  <tr>
   <td><code>table-header-group</code></td>
   <td><code>block</code></td>
  </tr>
  <tr>
   <td><code>table-footer-group</code></td>
   <td><code>block</code></td>
  </tr>
  <tr>
   <td><code>flex</code></td>
   <td><code>flex</code>, 다만 <code>float</code>&nbsp;은 이러한 요소에 효과가 없음</td>
  </tr>
  <tr>
   <td><code>inline-flex</code></td>
   <td><code>inline-flex</code>, 다만 <code>float</code>&nbsp;은 이러한 요소에 효과가 없음</td>
  </tr>
  <tr>
   <td><em>그외</em></td>
   <td><em>변화없음</em></td>
  </tr>
 </tbody>
</table>

> JavaScript에서 이 속성을 제어하려면 `cssFloat`라는 철자를 써야합니다. 또 IE8 이전버전에서는 `styleFloat`로 써야합니다.

## 값

#### `left`

요소가 자신의 포함 블록의 좌측에 떠(float) 있음

#### `right`

요소가 자신의 포함 블록의 우측에 떠 있음

#### `none`

요소가 떠있지 않음. 노말플로우를 따라감

#### `inline-start`

요소가 자신의 포함 블록의 시작쪽(start)에 떠 있음.

#### `inline-end`

요소가 자신의 포함 블록의 끝쪽(end)에 떠 있음.

> `inline-star`와 `inline-end`는 현재 FireFox에서만 작동됩니다.

[float의 속성 확인](https://codepen.io/Shim-SoYoung/pen/mvEbea)

---

## float 지우기(clear)

1. `clear:both`
   해당 블록에 `clear:both`를 줄 수 있습니다. 하지만 해당 블록 내에 `블록 형식 문맥`을 따르는 요소가 있다면 이 값은 작동하지 않습니다.

1. `float`

   `float`를 가진 자식 요소의 부모요소에 `float`를 적용해 줄 수 있습니다. 하지만 이 방법은 반응형 웹에 적합하지 않으므로 권장하지 않습니다.

1. `overflow`
   부동 요소가 담긴 컨테이너에(float를 준 요소의 부모 요소) `overflow:hidden`, `overflow:auto`를 주어서 블록 형식 문맥을 제한 할 수 있습니다.(만 auto 사용시 자식의 너비가 부모의 너비보다 크면 가로 스크롤바가 생기고, hidden의 경우 넘치는 부분이 잘리기 때문에 사용하지 않는 것이 좋습니다.)

> [블록 서식 문맥(block format context)는 웹 페이지의 블록 레벨 요소를 렌더링하는데 사용되는 CSS의 비주얼 서식 모델 중 하나이다.](https://developer.mozilla.org/ko/docs/Web/Guide/CSS/Block_formatting_context)

1. ★★가상요소 `::after` 사용
   `overflow`를 이용해서 float을 해제하는 것은 때때로 문제가 생길 수 있습니다.
   clearfix 핵을 이용해서 더 쉽게 제어할 수 있습니다.

부동요소가 담긴 컨테이너(float를 준 요소의 부모요소)에 아래의 `clearfix` 클래스를 주어 해제할 수 있습니다.

```css
.clearfix::after {
  content: "";
  clear: both;
  display: table;
}
```

clearfix를 준 요소 내부의 마지막에 내용이 빈(content: '') 테이블을(display: table) 만들고,

float: left, float: right를 초기화 시키겠다는 뜻입니다.

여기서 display: table 대신 display: block을 쓰는 것도 가능합니다.

> CSS2에서는 가상클래스(`:hover`, `:link`)와 가상요소(`:after`, `:before`)모두 싱글콜론(:)을 사용했지만 CSS3부터는 둘을 구분하기위해 가상클래스는 싱글콜론(:), 가상요소는 더블콜론(::)을 사용합니다.

[float 지우기](https://codepen.io/Shim-SoYoung/pen/KJMPmg)

#### 참고 링크

[w3school-CSS-float](https://www.w3schools.com/css/css_float.asp)

# position

요소 배치 방법을 지정합니다. `top`, `right`, `bottom`, `left` 속성들을 이용해 요소가 최종적으로 배치 될 위치를 지정합니다.

## 값

#### `position : static` (기본값)

기본적인 요소의 배치 순서에 따라 일반적인 흐름(normal flow)으로 배치됩니다.

`top`, `right`, `bottom`, `left` 속성을 사용할 경우에는 무시됩니다.

#### `position : relative` (상대 위치)

일반적인 흐름(normal flow)을 따라 배치됩니다.

기본 위치를 기준으로 `top`, `right`, `bottom`, `left` 속성을 이용해 이동할 수 있습니다.
(아무 속성을 주지 않으면 static과 동일하게 동작합니다.)

이 때 요소의 좌표는 다른 요소들의 위치에 영향을 주지 않습니다. 따라서 페이지 레이아웃에서 요소에게 지정된 공간은 static일 때와 동일합니다.

`top`,`bottom` 속성은 기본 위치에서부터 수직 방향으로 얼만큼 떨어지는 곳에 위치할 것인가를 설정합니다

`left`, `right` 속성은 기본위치에서부터 수평 방향으로 얼만큼 떨어지는 곳에 위치할 것인가를 설정합니다.

> top : 위를 기준으로 10px 움직인다(아래로)
> bottm : 아래를 기준으로 10px 움직인다(위로)
> left: 왼쪽을 기준으로 10px 움직인다(오른쪽으로)
> right : 오른쪽을 기준으로 10px 움직인다(왼쪽으로)

#### `position: fixed` (고정위치) IE 7 이상

요소가 일반적인 흐름(normal flow)에서 제거되고 블록 서식 문맥을 따라갑니다.

페이지 레이아웃에서 요소에 대한 공간이 생성되지 않습니다.

대신 `스크린의 뷰포트(viewport)를 기준으로 한 위치`에 배치됩니다.

부모 요소에 관계없이 브라우저 표시영역을 기준으로 `top`, `right`, `bottom`, `left` 속성을 사용해 이동합니다. 스크롤을 이동해도 항상 같은 위치에 고정됩니다.

상단에 고정된 navigation bar 나 세로로 긴 페이지에서 최상단으로 이동하는 TOP버튼을 만들 때 사용됩니다.

새로운 stacking context(쌓임 맥락)을 생성합니다.

> [쌓임 맥락](https://developer.mozilla.org/ko/docs/Web/CSS/Understanding_z-index/The_stacking_context)

#### `position : absolute` (절대위치)

요소가 일반적인 흐름(normal flow)에서 제거되고 블록 서식 문맥을 따라갑니다.

페이지 레이아웃에서 요소에 대한 공간이 생성되지 않습니다.

가장 가까이 있는 부모 요소(static 제외)를 기준으로 `top`, `right`, `bottom`, `left` 만큼 이동합니다. 부모 요소에 relative, absolute, fixed, sticky 속성이 선언되어 있으면 부모를 기준으로 하고, 부모에 해당 속성이 선언되어있지 않으면 body를 기준으로 합니다.

새로운 stacking context(쌓임 맥락)을 생성합니다.

#### `position : sticky` IE 지원되지않음

relative와 fixed의 하이브리드입니다.

요소가 일반적인 흐름(normal flow)을 따라 배치됩니다.

그 후에 `top`, `right`, `bottom`, `left` 값을 이용해 임계값을 설정할 수 있습니다.

```css
div {
  position: sticky;
  top: 10px;
}
```

위 코드는 뷰포트가 스크롤되어 요소가 상단으로부터 10px 미만이 될 때까지 상대적으로 `<div>`를 배치합니다. 하지만 그 임계값(10px)을 넘는 순간 `<div>`는 상단에서부터 10px이 되는 위치에 고정됩니다.

새로운 stacking context(쌓임 맥락)을 생성합니다.

_codepen에서 스티키는 안되네요_

[position 속성 확인](https://codepen.io/Shim-SoYoung/pen/LqZYvG)

[sticky 예제 확인](https://gedd.ski/post/position-sticky/)
