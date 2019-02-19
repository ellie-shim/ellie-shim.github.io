---
layout: post
title: "6주차- SVG, Canvas"
subtitle: "siots"
categories: siots
tags: topic
comments: true
---

# 6주차 topic - SVG, Canvas

# svg

많이 보긴 했는데 svg가 몰까??????

Scalable Vector Graphics 바로 확장 가능한 벡터 그래픽 이라고 합니다

MDN이 말하기를,
`2차원의 벡터 그래픽을 기술하기 위한 XML 마크업 언어이다.`

그래픽을 마크업하는 특수언어라네요. 그리고 W3C 표준입니당!

svg는 안되는 버전 빼고는 다 사용 가능합니다. 여기서 안되는 버전이란? 모두 아는 그것^^

[can i use - svg 지원 현황](https://caniuse.com/#feat=svg)

완벽한 웹 사이트를 위해서는 파일 용량을 줄여 성능을 높여야 합니다. 웹상에 아이콘, 로고, 일러스트레이션 이미지 등을 사용한다면 svg를 사용하는 것이 유일한 방법입니다.

svg는

1. 모든 스크린에서 화질이 선명하며,
2. 최소 용량이고,
3. 편집과 수정이 쉽다는 장점이 있습니다

svg는 벡터 그래픽 편집기를 이용하거나, 직접 코드를 작성해서 만들 수 있습니다.

> 벡터 그래픽 편집기에는 일러스트레이터, 스케치, Inkscape(무료), 포토샵(shape레이어를 사용하는 경우)이 있습니다.

## 구현 옵션

svg를 구현하는 데에는 몇가지 방법이 있습니다.

알아보기전에 [TheNounProject](https://thenounproject.com/#)에서 맘에드는 아이콘 하나를 pick 해봅시다

png로 다운받는 흑우 업쥬? svg로 픽 하세요

#### Img

일반 이미지처럼 사용하기. 이 방법은 조작 기능을 제한합니다.

```html
<img src="siots.svg" alt="siots" />
```

#### Background-image

background로 사용하기. 다운로드하는 동안 나머지 스타일 로딩을 차단시키기 때문에 사용하지 않는 편이 좋습니다.

이 방법은 조작 기능을 제한합니다.

```css
.logo {
  background-image: url(siots.svg);
}
```

#### Iframe

`<iframe>` 요소 내 svg를 로드할 수 있습니다. 대부분의 작업을 구현할 수 있지만, 더 발전적인 기능을 사용하고자 한다면 가장 좋은 방법은 아닙니다.

```html
<iframe src="siots.svg">Your browser does not support iframes</iframe>
```

#### Embed

`<embed>` 요소는 '외부 응용프로그램', '대화형 콘텐츠'를 통합할 때 사용됩니다. svg를 구현할 수는 있지만 사용하지 않는 편이 낫습니다.

```html
<embed type="image/svg+xml" src="siots.svg" />
```

#### 🐣 Object 🐣

`<object>` 요소는 HTML문서 내에 직접 내장시키지않고 svg를 조작하는 경우에 가장 좋은 방법입니다.

```html
<object type="image/svg+xml" data="siots.svg"
  >현재 브라우저는 iframe을 지원하지 않습니다.</object
>
```

#### Inline

svg 코드를 인라인하면 http 요청은 저장되지만, 이미지는 브라우저에 캐시되지 않습니다. 조작이 가장 쉬운 방법이지만, 인라인 svg코드를 유지하는 것은 어려울 수 있습니다.

```html
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 68 65">
  <path
    fill="#1A374D"
    d="M42 27v-20c0-3.7-3.3-7-7-7s-7 3.3-7 7v21l12 15-7 15.7c14.5 13.9 35 2.8 35-13.7 0-13.3-13.4-21.8-26-18zm6 25c-3.9 0-7-3.1-7-7s3.1-7 7-7 7 3.1 7 7-3.1 7-7 7z"
  />
  <path
    d="M14 27v-20c0-3.7-3.3-7-7-7s-7 3.3-7 7v41c0 8.2 9.2 17 20 17s20-9.2 20-20c0-13.3-13.4-21.8-26-18zm6 25c-3.9 0-7-3.1-7-7s3.1-7 7-7 7 3.1 7 7-3.1 7-7 7z"
  />
</svg>
```

#### 결론

SVG를 최대한 활용하려면 `<object>`를 사용하세요. 이미지처럼 동일하게 사용하려면 `<img>`나 `background-image`를 사용하세요.

<table>
  <thead>
    <tr>
      <th></th>
      <th>Object</th>
      <th>Inline</th>
      <th>Img</th>
      <th>Background-image</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th class="feature">CSS 조작</th>
      <td>가능</td>
      <td>가능</td>
      <td>일부 inline</td>
      <td>일부 inline</td>
    </tr>
    <tr>
      <th class="feature">JS 조작</th>
      <td>가능</td>
      <td>가능</td>
      <td>불가능</td>
      <td>불가능</td>
    </tr>
    <tr>
      <th class="feature">SVG 조작</th>
      <td>가능</td>
      <td>가능</td>
      <td>가능</td>
      <td>가능</td>
    </tr>
    <tr>
      <th class="feature">인터렉티브 SVG 애니메이션</th>
      <td>가능</td>
      <td>가능</td>
      <td>불가능</td>
      <td>불가능</td>
    </tr>
  </tbody>
</table>

## Element 요소와 요소가 갖고있는 속성

아래는 svg에서 쓰이는 요소들과 그 요소가 갖고있는 속성들입니다.

#### svg 선언

```js
<svg version="1.1"  width="400" height="400" xmlns="http://www.w3.org/2000/svg">
  //  그림그리기
</svg>
```

#### `<rect>`

사각형 그리기

1. `x` : 사각형의 좌측 상단의 x 값
1. `y` : 사각형의 좌측 상단의 y 값
1. `rx` : 사각형의 둥근 꼭짓점의 x방향으로의 반지름 (`rx`, `ry` 둘 중 하나만 명시하면 두 속성이 같은 값으로 설정 됨.)
1. `ry` : 사각형의 둥근 꼭짓점의 y방향으로의 반지름

```html
<rect x="60" y="10" rx="10" ry="10" width="30" height="30" />
```

#### `<circle>`

원 그리기

1. `r` : 원의 반지름
1. `cx` : 원의 중심을 기준으로 x축 값
1. `cy` : 원의 중심을 기준으로 y축 값

```html
<circle cx="25" cy="75" r="20" />
```

#### `<ellipse>`

타원 그리기

중심좌표와 x와 y의 반지름을 이용하여 타원을 생성할 수 있습니다.

1. `rx` : 타원의 x방향으로의 반지름 길이
1. `ry` : 타원의 y방향으로의 반지름 길이
1. `cx` : 타원의 중심을 기준으로 x축 값
1. `cy` : 타원의 중심을 기준으로 y축 값

```html
<ellipse cx="75" cy="75" rx="20" ry="5" />
```

#### `<line>`

직선 그리기.

선의 시작과 끝 지점을 지정하는 두 점을 속성으로 갖습니다.

1. `x1` : 점 1의 x값
1. `y1` : 점 1의 y값
1. `x2` : 점 2의 x값
1. `y2` : 점 2의 y값

```html
<line x1="10" x2="50" y1="110" y2="150" />
```

#### `<polyline>`

연결된 직선들의 그룹.

포인트들의 목록인 각 숫자들은 공백, 쉼표, 줄바꿈문자, EOL(end of life??)로 구분됩니다. 

1. points : 점들의 묶음

각 포인트는 반드시 x좌표와 y좌표를 가지고있어야합니다.(밑에는 하나 없는데..된다..?)

```html
  <polyline fill="none" stroke="red" points="236 , 133 221, 153 196, 153 212, 175 199, 203 234, 186 265, 203 259, 175 272,155 245,154,236 133 "/>
```

#### `<polygon>`

다각형.

점을 연결하는 직선으로 구성된다는 점에서 `polyline`과 매우 유사합니다. 하지만 `polygon`의 경우 자동으로 마지막 포인트로부터 첫번째 포인트로 직선을 만들어서 닫힌 모양을 만듭니다. (패스가 자동으로 닫힌다.)

1. points

```html
<polygon fill="violet" stroke="#fff" points="236,133 221,153 196,153 212,175 199,203 234,186 265,203 259,175 272,155 245,154"/>
```

#### `<path>`
`path` 엘리먼트는 svg 기본 도형 중 가장 강력한 엘리먼트입니다. `path`를 이용해서 선과 곡선, 호 등 여러가지를 그릴 수 있습니다. 모든 종류의 모양과 베지에 곡선, 2차원 곡선 등이 가능합니다.

1. d

`path`는 `d` 속성 하나로 정의됩니다.

예제는 아래처럼 생겼는데,
```html
<path d="M 20 230 Q 40 205, 50 230 T 90230"/>
```

`d` 속성 안에서 여러가지 명령어와 파라미터로 그리기 때문에 아주 복잡합니다.

path를 마스터하고싶은 분들은 [MDN-Path](https://developer.mozilla.org/ko/docs/Web/SVG/Tutorial/Paths)로 가서 더 많은 명렁어를 확인해보세요..넘많고..어렵고..난안할래..

#### `<text>`

text 기능..

1. x : 좌표
1. y
1. text-anchor : `start`, `middle`, `end` 텍스트의 중심점

css에서 사용하는 text-family등의 어트리뷰트들을 사용할 수 있습니다

```html
<text x="10" y="10">Hello siots</text>
```

`text` 안에서 `<tspan>` 이라는 애를 쓸 수 있습니다.
```html
<text>
  This is <tspan font-weight="bold" fill="red">bold and red</tspan>
</text>
```


## Attribute 속성

위에는 엘리먼트가 갖고있는 속성이었고 이번에 볼 속성은 공통 속성입니다.

#### fill 색 채우기
#### stroke 선 그리기
#### fill-opacity 칠의 투명도
#### stroke-opacity 선의 투명도

```html
<rect x="10" y="10" width="100" height="100" stroke="blue" fill="purple"
       fill-opacity="0.5" stroke-opacity="0.8"/>
```

#### stroke-width 선 두께

#### stroke-linecap 선의 마무리?

값으로는 `butt`, `square`, `round`가 있습니다.

![stroke-linecap](https://developer.mozilla.org/@api/deki/files/355/=SVG_Stroke_Linecap_Example.png)

```html
  <line x1="40" x2="120" y1="20" y2="20" stroke="black" stroke-width="20" stroke-linecap="butt"/>
  <line x1="40" x2="120" y1="60" y2="60" stroke="black" stroke-width="20" stroke-linecap="square"/>
  <line x1="40" x2="120" y1="100" y2="100" stroke="black" stroke-width="20" stroke-linecap="round"/>
```

#### stroke-linejoin

선이 꺾일 때의 처리...?ㅎㅎ 말그대로 라인이 쪼인할때,,ㅎㅎ

값으로는 `miter`, `round`, `bevel`이 있습니다.

![stroke-linejoin](https://developer.mozilla.org/@api/deki/files/356/=SVG_Stroke_Linejoin_Example.png)

```html
<polyline points="40 220 80 180 120 220" stroke="black" stroke-width="20" stroke-linecap="square" fill="none" stroke-linejoin="bevel"/>
```

#### stroke-dasharray
점선의 거리...?ㅎㅎㅎ 

만약 값이 `"5,5,20"`이라면 

5 fill, 5 empty, 20 fill, 5 empty, 5 fill, 20 empty, 5 fill, 5 empty, 20 fill..

```html
<path d="M 10 75 Q 50 10 100 75 T 190 75" stroke="black" stroke-linecap="round" stroke-dasharray="5,10,5" fill="none"/>
<path d="M 10 75 L 190 75" stroke="red" stroke-linecap="round" stroke-width="1" stroke-dasharray="5,5" fill="none"/>
```

## style 사용하기

svg 요소에 대한 속성들을 설정할 때 style을 사용할 수 있습니다.

이런식으로 말이져
```html
<rect x="10" height="180" y="10" width="180" style="stroke: black; fill: red;"/>
``` 

## id, class 주기

svg 요소에 id나 class 이름을 설정해주고 css에서 제어할 수 있습니다. css에서 제어할 수는 있지만 css에서 사용하는 어트리뷰트들은 사용할 수 없습니다. svg의 어트리뷰트만 사용할 수 있습니다.


## 그 외
위에서 몇가지 정리했지만 너무 많기도 하고 미번역^^이라 일부 속성만 가져왔습니다. 

그 외에 아래의 속성들도 있으니 확인해보세용

1. Gradients
1. Patterns
1. Texts
1. Basic Transformations
1. Clipping and masking
1. Other content in SVG
1. Filter effects
1. SVG fonts
1. SVG Image tag
1. Tools for SVG
1. SVG and CSS
[그 외의 것들은 여기서 확인해보세요 미번역..MDN 튜토리얼](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial)

## 간지템🐾🐾
[간지템 확인해보세요](https://codepen.io/Shim-SoYoung/pen/YBBweN)

## 🐾🐾결론 : svg는 일러스트레이터로 만들자.ㅎㅎ🐾🐾

# Canvas

canvas는 요소마다 브라우저를 좀 타는거 같네요 [canIUse](https://caniuse.com/#search=canvas)에서 확인 후 사용합시다.


캔버스에 그림을 그리려면 자바스크립트 컨텍스트 오브젝트를 사용하며....
![띠용](http://attach.s.op.gg/forum/20180227231047_998034.jpeg)


## `<canvas>`

```html
<canvas id="siots" width="150" height="150">
  <img src="images/clock.png" width="150" height="150" alt=""/>
</canvas>
```

- canvas를 선언해주고 그림을 그릴 수 있습니다.

- `width`와 `height` 두가지 속성이 있습니다. 크기를 직접 지정해주지 않으면  기본값인 300px * 150px로 설정됩니다. => css상에서 width와 height를 설정해주면 렌더링이 왜곡된 것 처럼 보이는 경우가 있다고 합니다.

- canvas에는 id나 class 를 설정해줄 수 있는데, 대체로 항상 id 속성을 사용해주는 것이 좋습니다. 스크립트 내에서 구분을 쉽게 할 수 있기 때문입니당.

- canvas 요소는 일반적인 이미지처럼 스타일을 적용할 수 있습니다(margin, border, background 등). 하지만 이 스타일은 캔버스 위에 그리는것엔 영향을 끼치지 않습니다. 캔버스 자체의 스타일링이 됩니다.

- canvas를 지원하지 않는 브라우저를 위해 대체 콘텐츠를 작성해주어야합니다. canvas 태그 안에 대체 콘텐츠를 삽입하면, 지원하지 않는 브라우저는 내부의 콘텐츠만을 렌더링합니다.

- `</canvas>` 닫는 태그는 필수입니다.

## `getContext()`

`getContext()` 메소드를 이용해서 렌더링 컨텍스트 타입을 지정합니다. 

잘 모르겠는데 타입은 2d냐 3d냐 인듯합니다

아래처럼 코드를 작성해 사용합니다.

이렇게 컨텍스트 타입을 지정해주어야 드뤄잉을 할수있슴니다~~

```js
const canvas = document.querySelector('#siots');
var ctx = canvas.getContext('2d');
```

이 메소드를 이용해 해당 브라우저에서 canvas를 지원하는지 안하는지를 확인할 수 있습니다

```js
var canvas = document.getElementById('#siots');

if (canvas.getContext){
  var ctx = canvas.getContext('2d');
  // drawing code here
} else {
  // canvas-unsupported code here
}
```
이렇게 말이죵

재밌죵!!!!!!!!!!!!!!?

[codepen에서 canvas를 만지작 해봅시당](https://codepen.io/Shim-SoYoung/pen/bzZegN)

## 직사각형 그리기

#### fillRect(x, y, width, height)
색칠된 직사각형을 그립니다.

#### strokeRect(x, y, width, height)
직사각형 윤곽선을 그립니다.

#### clearRect(x, y, width, height)
특정 부분을 지우는 직사각형이며, 이 지워진 부분은 완전히 투명해집니다.

> 색칠된 직사각형을 그리는거라 색칠을 먼저 해줘야되나봐용


## 제성합니다...
![흑](http://2runzzal.com/media/MUU0QXF5Uis2TVFZdjVTNU85eCtHQT09/thum.png)

흐르륵흐르르륵흐르흐르륵 

canvas는 배우려면 시간이 많이 필요할 것 같아요 svg를 조금만 하고 canvas를 팔것을 그랬어요.. 그래서 canvas는 다음에 다시 할게요,,,

다음에..다시..돌아온다.. 
![ㄹ](https://i.pinimg.com/originals/bf/ad/10/bfad108fd51b5226686aec2a3ce48c13.jpg)

[디자인을 참아낼 수 있다면](http://www.soen.kr/)
[영어를 읽을 수 있다면](https://developer.mozilla.org/ko/docs/Web/HTML/Canvas/Tutorial)


# CSS 선택자

#### 1. 하위 선택자

.myDiv 아래의 **모든** `p`태그 선택

```css
.myDiv p
```

#### 2. 자식 선택자

.myDiv 바로 아래의(자식) `p` 태그만 선택

```css
.myDiv > p
```

#### 3. 형제 선택자

.myDiv의 형제 요소중 `p` 태그만 선택

```css
.myDiv ~ p
```

#### 4. 인접 형제 선택자

.myDiv의 **첫번째 형제가 p일 경우.**

.myDiv의 첫번째 형제가 h1이고 두번째 형제가 p라면 해당되지 않습니다.

```css
.myDiv + p
```

[형제선택자, 인접형제선택자](https://codepen.io/Shim-SoYoung/pen/MLxwQY)





#### 출처

[https://svgontheweb.com/ko/](https://svgontheweb.com/ko/)
[svg 튜토리얼 - MDN](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial)
[canvas 튜토리얼 - MDN](https://developer.mozilla.org/ko/docs/Web/HTML/Canvas/Tutorial)
