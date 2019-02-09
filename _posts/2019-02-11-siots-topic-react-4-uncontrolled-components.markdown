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

```js
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    // input에 onChange가 일어날 때마다 value값을 setState 해준다.
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

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
    alert('A name was submitted: ' + this.input.value);
    event.preventDefault();
  }

  render() {
    return (
      // 1. ref 설정
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" ref={(input) => this.input = input} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```
진리의 원천을 DOM에 두기 때문에, 