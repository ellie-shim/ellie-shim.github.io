---
layout: post
title: "5주차- REACT - 3 - Ref"
subtitle: "siots"
categories: siots
tags: topic
comments: true
---

# 5주차 topic - 

# Ref(Reference 참조)와 DOM

prop으로 사용할 수 없는 것에는 `key`와 `ref`가 있었습니다. 기억나나요?

Ref는 render 메소드에서 생성된 DOM 노드 혹은 React 엘리먼트 객체에 접근할 수 있는 방법을 제공합니다.

전형적인 React 데이터 흐름에서는 부모 컴포넌트에서 자식 엘리먼트를 조작하기 위해 `props`만을 사용합니다. 하지만 가끔은 자식을 명령형으로 변경해야 할 필요가 있습니다. 그러면 어떠한 상황에 DOM에 직접적인 접근이 필요할까요?

## 1. 언제 ref를 사용해야 하나요?
1. input/textarea 등에 포커스를 해야할 때
1. 포커스, 텍스트 선택영역, 혹은 미디어의 재생을 관리할 때
    - DOM API 메소드로만 가능
1. 명령형 애니메이션을 발동시킬 때
1. 특정 DOM의 크기를 가져와야 할 때
1. 특정 DOM에서 스크롤 위치를 가져오거나 설정을 해야 할 때
1. 외부 라이브러리(플레이어, 차트 등)를 사용 할 떄

## 2. Ref의 남용은 금물입니다.

ref를 사용하기 전에, 앱의 상태를 컴포넌트 계층의 어떤 부분에서 소유해야 하는지를 다시 한 번 생각해보세요. 많은 경우 적절한 장소는 계층의 상위에 있는 컴포넌트일 것입니다.

ref를 사용하면 코드를 간결하게 짤 수 있지만, state와 props로 해결할 수 있는 부분에서는 ref를 사용하지 않는 것이 유지보수에 좋습니다.

## 3. Ref 사용하기

ref를 사용하는 방법에는 세가지가 있습니다.

### 1. 문자열 attribute 사용 

- 구식 방법이라 잘 사용하지 않습니다만 간단하게 예제로 확인하겠습니다.

```js
class RefExample extends React.Component {
  render() {
    return (
      <div>
        <input ref = 'myInput' />
      </div>
    );
  }

  componentDidMount() {
    this.refs.myInput.value = 'Hi, I used ref to do this.';
    this.refs.myInput.placeholder = 'input placeholder';
  }
}

ReactDOM.render(<RefExample />, document.getElementById('root'));
```
- 컴퍼넌트에 `ref = 'refName'` 형식으로 ref를 지정합니다.
- 문자열 형식으로 만든 ref는 `this.refs.refName`으로 접근해야 합니다.
- refs를 사용할 때는 컴퍼넌트가 렌더링 된 이후여야 합니다.

### 2. 콜백 함수 사용

- React 16.3 버전 이하에서 사용하는 `callback ref`입니다.(강사님이 번역도 안해주신것을 보면...^^)

- [![Edit ref-콜백함수이용](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/9yv3o8jxly)

```js
class RefExample extends React.Component {
  handleClick() {
    // 3. textBox의 input의 value 값을 설정해주는 함수입니다.
    this._textBox._input.value = "I used ref";
  }

  render() {
    return (
      <div>
        // 2. TexoBox _textBox이라는 이름의 ref를 붙여줍니다.
        <TextBox ref={box => this._textBox = box} />
        <button onClick={this.handleClick.bind(this)}>Click Me</button>
      </div>
    );
  }
}

class TextBox extends React.Component {
  render() {
    return (
      // 1. input에 _input이라는 이름의 ref를 붙여줍니다.
      <input ref=  { ref => this._input = ref} />
    );
  }
}

const rootElement = document.getElementById("root");
ReactDOM.render(<RefExample />, rootElement);
```

### 3. `React.createRef()` 사용

- React 16.3 버전에서 도입된 기능입니다.


#### Ref 생성하기

Ref는 `React.creatRef()`를 통해 생성한 뒤 React 엘리먼트의 ref 어트리뷰트에 붙여줄 수 있습니다.

```js
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    // ref 생성
    this.myRef = React.createRef();
  }
  render() {
    // 엘리먼트의 ref 어트리뷰트에 붙여줌
    return <div ref={this.myRef} />;
  }
}
```
`React.createRef()` 라는 함수를 실행하면 객체가 생성되고, 이 객체는 붙여준 DOM 객체 가리킵니다(화살표 참조합니다)

#### Ref 사용하기

`render` 메소드에서 반환하는 엘리먼트에 ref가 넘겨지면(어트리뷰트에 붙여주어 연결해주면), ref의 `current` 속성을 통해 해당 노드에 접근할 수 있게 됩니다(연결된 DOM 노드를 가져올 수 있습니다)

```js
const node = this.myRef.curret
```

ref의 값은 노드의 유형에 따라 달라집니다.

- HTML 엘리먼트에 `ref` 어트리뷰트가 사용되면, ref의 `current` 속성은 DOM 엘리먼트 객체를 가리킵니다.

- 클래스 컴포넌트에 `ref` 어트리뷰트가 사용되면, ref의 `current` 속성은 해당 컴포넌트로부터 생성된 인스턴스를 가리킵니다.(클래스 컴포넌트를 생성하면 자동으로 인스턴스가 생성되고 `this`는 이 인스턴스를 기리킵니다.)

- **함수형 컴포넌트는 인스턴스를 가질 수 없기 때문에 ref 어트리뷰트 역시 사용할 수 없습니다**


#### DOM 엘리먼트에 ref 사용하기

```js
class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);
    // input DOM 엘리먼트에 접근하기 위해 ref를 만들었습니다.
    this.textInput = React.createRef();
    // bind를 이용해서 this 고정
    this.focusTextInput = this.focusTextInput.bind(this);
  }

  focusTextInput() {
    // DOM API를 사용해서 명시적으로 input에 포커스를 두는 코드입니다.
    // 주의: "current" 속성을 사용해 DOM 노드에 접근하고 있습니다.
    this.textInput.current.focus();
  }

  render() {
    return (
        // <input> ref와 `textInput`을 연결해주었습니다.
      <div>
        <input
          type="text"
          ref={this.textInput} />

        <input
          type="button"
          value="Focus the text input"
          onClick={this.focusTextInput}
        />
      </div>
    );
  }
}
```

React는 컴포넌트가 마운트 되면 `textInput`의 `current` 속성에 DOM 엘리먼트 객체를 할당하며, 언마운트가 되었을 떄 다시 `null`로 되돌립니다. 이는 인스턴스가 저장된 경우의 메모리 누수를 방지합니다.

`ref`의 갱신은 `componentDidMount`와 `componentDidUpdate` 라이프사이클 훅 직전에 일어납니다.


#### 클래스 컴포넌트에 ref 사용하기

```js
class AutoFocusTextInput extends React.Component {
  constructor(props) {
    super(props);
    // ref를 생성했습니다.
    this.CustomInput = React.createRef();
  }

  componentDidMount() {
    // CustomInput ref를 가진 인스턴스의 focusTextInput() 함수를 실행합니다.
    this.CustomInput.current.focusTextInput();
  }

  render() {
    return (
      // CustomInput ref를 연결해주었습니다.
      <CustomTextInput ref={this.CustomInput} />
    );
  }
}
```

DOM 엘리먼트에 ref 사용하기 파트의 예제에 있는 `CustomTextInput` 컴포넌트를 감싸는 새 컴포넌트를 만들었습니다.

`CustomTextInput` 인스턴스에 접근하기 위해 ref를 생성해 연결했고, `focusTextInput`을 직접 호출했습니다.

**컴포넌트의 인스턴스를 가리키기 위해 ref를 사용하는 것은 컴포넌트가 클래스로 선언되었을 때에만 동작합니다.**

**함수형 컴포넌트는 인스턴스를 가질 수 없기 때문입니다.**

**다만, 함수형 컴포넌트 안에서 ref 어트리뷰트를 사용하는 것은 얼마든지 가능합니다.**

```js
function CustomTextInput(props) {
  // textInput은 반드시 여기에서 선언되어야 합니다.
  let textInput = React.createRef();

  function handleClick() {
    textInput.current.focus();
  }

  return (
    <div>
      <input
        type="text"
        ref={textInput} />

      <input
        type="button"
        value="Focus the text input"
        onClick={handleClick}
      />
    </div>
  );
}
```

