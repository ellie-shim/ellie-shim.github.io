---
layout: post
title: "5주차- REACT - 5 - 성능 최적화"
subtitle: "siotz"
categories: siotz
tags: topic
comments: true
---

# 5주차 topic - 

# 성능 최적화

🐰🐤🐣🐼🐈🐾🐾🐾🐾🐾🐾🐾🐾

React 어플리케이션의 속도를 높이는 몇가지 방법을 알아보겠습니다.


## 1. 프로덕션 빌드 사용하기

앱을 개발할 때에는 개발 모드를 사용하고, 배포할 때에는 프로덕션 모드를 사용해야 합니다.

create-react-app을 이용해서 만든 경우와 직접 webpack을 설정한 경우에 따르는 방법이 다릅니다.

## 2. Chrome 퍼포먼스 탭에서 컴포넌트 프로파일링

Chrome 개발자도구의 퍼포먼스 탭에서 컴포넌트의 마운트, 업데이트, 언마운트를 시각적으로 볼 수 있습니다.

실수로 무의미한 UI가 얼마나 업데이트 되는지, UI가 얼마나 자주 업데이트 되는지를 살펴볼 수 있습니다.

자세한 동작은 [Ben Schwarz의 아티클](https://building.calibreapp.com/debugging-react-performance-with-react-16-and-chrome-devtools-c90698a522ad)을 참조하세요.

## 3. 긴 리스트 가상화하기

만약 어플리케이션이 긴 목록 데이터(수백 혹은 수천개 행)를 렌더링 해야한다면, `윈도윙(windowing)`이라는 기술 사용을 권장합니다. 이 기술은 주어진 시간 내에 행의 작은 부분만 렌더링하므로 컴포넌트를 다시 렌더링 하는데 걸리는 시간과 생성된 DOM 노드 갯수를 크게 줄일 수 있습니다.

[React Virtualized](https://bvaughn.github.io/react-virtualized/#/components/List) 는 유명한 윈도잉 라이브러리입니다. 목록, 그리드, 표 데이터를 표현하기 위한 여러가지 재사용가능한 컴포넌트를 제공합니다



## 4. shouldComponentUpdate

React는 setState()가 일어난 컴포넌트의 모든 자식 엘리먼트들을 새로 구축합니다.
구축하며 상태로부터 화면을 어떻게 그려야하는지 알아내야하기때문에 모든 `render()` 메소드를 다시 다 호출해봅니다.


때문에 위쪽에 있는 컴포넌트(App과 같은)에서 상태가 자주 바뀌게 되면, 많은 자식들의 `render()` 메소드가 다 호출되기 때문에 느려질 수 있습니다. 


props와 state는 모두 객체이고, 이 두가지가 바뀌지않았다면 화면을 새로 그릴 필요가 없습니다. 이러한 일부 상황에서 컴포넌트를 업데이트할 필요가 없는 경우  `shouldComponentUpdate` 에서 `false` 를 반환하여 이 컴포넌트 및 하위에서 호출하는 `render()` 를 포함한 전체 렌더링 프로세스를 스킵할 수 있습니다.

```js
shouldComponentUpdate(nextProps, nextState) {
  return true
  // 또는
  return false
}
```

예제
```js
class CounterButton extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: 1};
  }
  // 현재 state(prop)와 다음 state(prop)의 상태가 다를 경우에 
  // true를 반환하여 render() 메소드를  다시 호출합니다.
  shouldComponentUpdate(nextProps, nextState) {
    if (this.props.color !== nextProps.color) {
      return true;
    }
    if (this.state.count !== nextState.count) {
      return true;
    }
    return false;
  }

  render() {
    return (
      <button
        color={this.props.color}
        onClick={() => this.setState(state => ({count: state.count + 1}))}>
        Count: {this.state.count}
      </button>
    );
  }
}
```
이 코드에서 `shouldComponentUpdate` 는 `props.color` 나 `state.count` 에 어떤 변화가 있는지만 체크합니다. 이 값들이 변하지않으면 컴포넌트는 업데이트되지않습니다.

`PureComponent`에는 `shouldComponentUpdate` 라이프사이클 훅이  내장되어있어서 위의 작업을 간단하게 할 수 있습니다.

## 5. PureComponent

`shouldComponentUpdate`가 내장된 `PureComponent`로 다시 코드를 작성했습니다. 4번의 예제와 아래의 코드는 동일하게 동작합니다.

```js
class CounterButton extends React.PureComponent {
  constructor(props) {
    super(props);
    this.state = {count: 1};
  }

  render() {
    return (
      <button
        color={this.props.color}
        onClick={() => this.setState(state => ({count: state.count + 1}))}>
        Count: {this.state.count}
      </button>
    );
  }
}
```

다른 예제에서 좀 더 확인해보겠습니다. 내가 input 필드에 입력한 값을 아래에 출력해주는 예제입니다. 

[![Edit 퓨어컴포넌트-상태최적화 예제](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/xz3x93443p)


하지만 `shouldComponentUpdate`나 `PureComponent`는 **얕은 비교만 수행하므로, 깊은 비교가 일어나는 props와 state의 변경에서는 사용할 수 없습니다.**

또 복잡한 데이터 구조에서 문제가 될 수 있으므로 이전 값과 새로운 값을 잘 확인하며 코드를 작성해야 합니다.

🐈🐾🐾🐾🐾🐾🐾🐾🐾

> 자바스크립트에는 원시타입과 참조타입이 있습니다.
> number, string, boolean, null, undefined는 원시타입이고 불변입니다.
> object, array, function은 참조타입입니다.

[![Edit 상태최적화 예제-참조가 바뀌지 않을 때](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/n0w9p0lqj4)

예제를 보겠습니다.

내가 input 필드에 입력한 값이 아래에 차례대로 출력됩니다.

입력한 값은 이전 상태의 배열에 push하고, push 된 배열이 다음 상태에 들어갑니다.

하지만  코드는 제대로 동작되지 않을것입니다. 배열은 참조타입이고 가변형이지만, PureComponent는 얕은 비교를 하기 때문에 배열의 참조만 비교 될 것입니다.

이 예제에서 깊은 비교를 하도록 코드를 다시 작성할 수도 있습니다. 
하지만 우리는 `다시 그릴 필요가 없는 부분은 그리지 않으며` 최적화를 하고 있는 것인데, 깊은 비교(비싼 연산. 연산이 오래걸린다)를 한다면 최적화를 할 필요가 없어지는 것입니다.

그래서 PureComponent는 얕은 비교를 하며 아주 빠르게 동작합니다.


## 6. 불변성 

불변이 아닌 **값**(가변)이 변경되었는지 확인하려면 연산이 오래걸립니다.(비싼 연산)

어떤 값이 **내용이 바뀌면 무조건 참조가 바뀐다** 라고 하면(불변),

내용이 바뀌었는지 확인하려면 **참조가 바뀌었는지**만 확인하면 됩니다. 

그래서 깊은 비교를 할 필요 없이 얕은 비교로 참조만 확인 하고 내용 변경을 알 수 있습니다.

---

react.component를 상속받으면 `setState()`를 호출할 때 마다 `render()` 메소드를 다시 호출합니다(비싸다).

내용이 바뀌었을 때만 `render()` 메소드가 호출된다면 비용이 많이 줄어들 것입니다.

상태 안에 저장하는 값들을 불변한 값(값과 참조가 같이 바뀌는)인 것처럼 코딩하면 react는 얕은 비교만으로도 빠르게 비교하고 그릴 수 있습니다.

- 배열이나 객체가 들어왔을 때에는 꼭 복사해서 새 배열을 만들어 참조를 바꾸고 진행합니다.

하지만 매번 확인할 때마다 새 배열이나 새 객체를 만들어야하기 때문에 속도가 느리고 메모리가 소비됩니다.

매번 참조를 새로 설정해주는 번거로움이 있어서 라이브러리를 많이 사용합니다.

#### 라이브러리

1. [immutable-js](https://facebook.github.io/immutable-js/) 
  - List : 배열 같은 친구
  - Map : 객체 같은 친구
  - 내장된 객체와 배열 메소드를 쓸 수 없고 **라이브러리에서 설정한 메소드만** 사용할 수 있다.
  - [repl 확인](https://repl.it/@bbgrams/GaseousInnocentUpgrades)

1. [immer](https://github.com/mweststrate/immer)
  - 내장된 객체와 배열 메소드를 쓸 수 있다.
  - 요즘 떠오르는 불변값 라이브러리
  - 조시옷님🐤🐤🐤🐤🐤🐤🐤🐤🐤🐤🐤🐤

