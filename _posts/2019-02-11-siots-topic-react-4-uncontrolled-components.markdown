---
layout: post
title: "5주차- REACT - 4 - 제어되지 않는 컴포넌트"
subtitle: "siots"
categories: siots
tags: topic
comments: true
---

# 5주차 topic -

# 제어되는 컴포넌트 (Controlled Components)

퀵스타트에 있는 내용이니까 간단하게 볼게요!

`<input>`, `<textarea>`, `<select>` 같은 form 요소는 자기만의 상태를 가지고 사용자의 입력에 따라 업데이트됩니다. 반면에 React에서는, 변경 가능한 상태를 일반적으로 컴포넌트의 state 속성에 위치시키며, 이는 `setState()`로만 업데이트할 수 있습니다.

React state를 "진리의 유일한 원천 (single source of truth)"으로 만들어 두 세계를 결합할 수 있습니다. 이렇게 하면 사용자의 입력에 따라 폼에서 발생되는 일을 React 컴포넌트 측에서 제어하게 됩니다. 이런 방식으로, React에 의해 제어되는 폼 요소를 **"제어되는 컴포넌트"** 라고 부릅니다.

#### input, textarea 태그

```js
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = { value: "" };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    // input에 onChange가 일어날 때마다 value값을 setState 해준다.
    this.setState({ value: event.target.value });
  }

  handleSubmit(event) {
    alert("A name was submitted: " + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input
            type="text"
            value={this.state.value}
            onChange={this.handleChange}
          />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

#### select 태그

```html
<select>
  <option value="grapefruit">Grapefruit</option>
  <option value="lime">Lime</option>
  <option selected value="coconut">Coconut</option>
  <option value="mango">Mango</option>
</select>
```

`selected` 어트리뷰트 대신에 `select` 태그에 `value` 어트리뷰트를 사용해서 선택된 값을 설정해줍니다.

```js
class FlavorForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = { value: "coconut" };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({ value: event.target.value });
  }

  handleSubmit(event) {
    alert("Your favorite flavor is: " + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Pick your favorite La Croix flavor:
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="grapefruit">Grapefruit</option>
            <option value="lime">Lime</option>
            <option value="coconut">Coconut</option>
            <option value="mango">Mango</option>
          </select>
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

데이터를 변경하는 모든 방법에 대한 이벤트 핸들러를 작성해야하고, 또 하나의 React 컴포넌트에 모든 input state를 전달해야하기 때문에 제어되는 컴포넌트는 매우 귀찮은 작업일 수 있습니다.

기존 코드베이스를 React로 변경하거나, React 어플리케이션을 React가 아닌 라이브러리와 통합할 때 같은 상황에서 사용할 수 있는 대체 기술로 `제어되지 않는 컴포넌트` 가 있습니다.

# 제어되지 않는 컴포넌트 (Uncontrolled Components)

폼을 구현할 때에는 웬만하면 `제어되는 컴포넌트`를 권장합니다. 폼데이터가 React에 의해 적절히 제어될 수 있기 때문입니다.

반면 제어되지 않는 컴포넌트를 사용하면, 폼 데이터는 DOM 자체 기능에 의해 제어됩니다.

제어되지 않는 컴포넌트를 만들 때에는 상태 업데이트를 위해 이벤트 핸들러를 작성할 필요가 없습니다. `ref`를 사용해서 폼 데이터를 DOM으로부터 가져올 수 있습니다.

```js
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleSubmit(event) {
    // 2 .ref로부터 value 값 가져옴
    alert("A name was submitted: " + this.input.value);
    event.preventDefault();
  }

  render() {
    return (
      // 1. ref 설정
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" ref={input => (this.input = input)} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

진리의 원천을 DOM에 두기 때문에, React를 사용한 코드와 사용하지 않은 코드의 통합 작업을 좀 더 쉽게 만들어 줍니다. 또한 코드의 양이 상대적으로 적습니다.

지저분하더라도 빠른 해결책을 원한다면 제어되지 않는 컴포넌트를 이용하세요.

#### 기본값 지정하기

제어되지 않는 컴포넌트로 남겨두면서 초기값을 설정해주어야 할 때에는 `value` 어트리뷰트 대신 `defaultValue`를 사용해줍니다. `value` 값을 설정해주는 순간 제어되는 컴포넌트가 되기 때문입니다.

```js
render() {
  return (
    <form onSubmit={this.handleSubmit}>
      <label>
        Name:
        <input
          defaultValue="Bob"
          type="text"
          ref={(input) => this.input = input} />
      </label>
      <input type="submit" value="Submit" />
    </form>
  );
}
```

`<input type="checkbox">`와 `<input type="radio">` 엘리먼트는 `defaultChecked` 어트리뷰트를,

`<input>`, `<select>`, `<textarea>`는 defaultValue 어트리뷰트를 지원합니다.

```markdown
`<input type="checkbox">`, `<input type="radio">` : `checked={true}` 로 설정해주면 제어되는 컴포넌트가 됩니다.

`defaultChecked={true}` 로 제어되지않는 컴포넌트이면서 checked의 기본값이 true이게 설정할 수 있습니다.
```

#### <input type="file">

(MDN - File API)[https://developer.mozilla.org/en-US/docs/Web/API/File/Using_files_from_web_applications]

React에서 `<input type="file">`은 언제나 제어되지 않는 컴포넌트 입니다. 왜냐하면 이 엘리먼트의 값은 오로지 사용자에 의해서만 지정될 수 있기 때문입니다.

```js
class FileInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
  }
  // highlight-range{4-6}
  handleSubmit(event) {
    event.preventDefault();
    console.log(this.fileInput);
    // files 라는 곳에 fileList가 있습니다. fileList는 첨부 된 파일의 정보를 담고있습니다.
    console.log(this.fileInput.files);
    console.log(this.fileInput.files[0].name);
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Upload file:
          {/* highlight-range{1-6} */}
          <input
            type="file"
            ref={input => {
              this.fileInput = input;
            }}
          />
        </label>
        <br />
        <button type="submit">Submit</button>
      </form>
    );
  }
}
```

[![Edit input file - 제어되지 않는 컴포넌트](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/j20m79oj99)

코드샌드박스에서 console창을 확인해봅시다.

![this.refName.files에 들어있는 값](https://ellie-shim.github.io/assets/img/topic-5-file.png)

this.refName.files에 들어있는 값

[HTML5-HTML5 File API 기초부터 썸네일 이미지 생성까지](https://programmingsummaries.tistory.com/367) : 자바스크립트로 제어하는 옛날 글이긴 한데 나중에 참고해보세요

#### 😵 그럼 언제 제어되지 않는 컴포넌트를 써도 될까요 😵

🐰🐤🐣🐼🐾🐾🐾🐾🐾🐾🐾🐾
[제어되는 input과 제어되지 않는 input에 대한 글](https://goshakkk.name/controlled-vs-uncontrolled-inputs-react/)

위 글의 결론 :

모든 상황에서 제어되는 컴포넌트를 사용하는 것도 좋습니다만,
폼이 아주 간단하고 작동된다면 ref를 이용한 제어되지 않는 컴포넌트를 사용하는 것도 괜찮습니다.

또한 제어되지 않는 컴포넌트를 제어되는 컴포넌트로 변경하는 것은 어렵지 않습니다. ref를 나쁘다고만 생각하지 마세요.

<table>
  <thead>
    <tr>
      <th>feature</th>
      <th>제어되지않는<br />uncontrolled</th>
      <th>제어되는<br />ontrolled</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>one-time value retrieval (e.g. on submit)<br />일회성 값 (예 : 제출시)</td>
      <td>✅</td>
      <td>✅</td>
    </tr>
    <tr>
      <td><a href="https://goshakkk.name/submit-time-validation-react/">validating on submit<br />제출시에 유효성 확인(예 : 회원가입 페이지에서 input 입력 후 회원가입 버튼(submit)을 눌렀을 때 이름은 필수로 입력해주세요 같은 확인을 해줄 때 )</a></td>
      <td>✅</td>
      <td>✅</td>
    </tr>
    <tr>
      <td><a href="https://goshakkk.name/instant-form-fields-validation-react/">instant field validation<br/>입력 즉시 필드의 유효성 확인(예 : 회원가입 페이지에서 아이디를 8자 미만으로 적었을 때 8자 이상으로 적어달라고 체크 할 떄)</a></td>
      <td>❌</td>
      <td>✅</td>
    </tr>
    <tr>
      <td><a href="https://goshakkk.name/form-recipe-disable-submit-button-react/">conditionally disabling submit button<br />조건부로 제출 버튼 비활성화(예 : 회원가입 페이지에서 필수입력 폼이 비어져있을 때 회원가입 버튼 비활성화)</a></td>
      <td>❌</td>
      <td>✅</td>
    </tr>
    <tr>
      <td>enforcing input format <br />필수 input 형식</td>
      <td>❌</td>
      <td>✅</td>
    </tr>
    <tr>
      <td>several inputs for one piece of data <br />하나의 데이터에 대한 여러가지의 입력</td>
      <td>❌</td>
      <td>✅</td>
    </tr>
    <tr>
      <td><a href="https://goshakkk.name/array-form-inputs/">dynamic inputs <br />동적 입력</a></td>
      <td>❌</td>
      <td>✅</td>
    </tr>
  </tbody>
</table>
