---
layout: post
title: 자바스크립트 - 프로토타입
date: 2018-10-08 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: software.jpg # Add image post (optional)
tags: [Productivity, Software] # add tag
---

# 프로토타입(Prototype)

- 수많은 객체가 공통으로 사용하는 속성과 메소드를 중복해서 저장하는 것은 낭비이다.
```js
function personFactory(name){
    return{
        name,
        introduce : function(){
            return `안녕하세요. 제 이름은 ${this.name}입니다.`;
        };
    };
};

const people = [];
for( let i = 0; i <100; i++){
    people.push(personFactory('길동'))
}
people[0].introduce() // '안녕하세요. 제 이름은 길동입니다.
```

- JS에서는 객체간에 공유되어야 하는 속성과 메소드를 `프로토타입`이라는 기등을 이용해서 효율적으로 저장할 수 있다.
- 어떤 객체에 프로토타입을 지정하면, 프로토타입의 속성을 해당 객체에서 재사용 할 수 있다.

## 프로토타입 지정 방법
1. `Object.create` 함수
```js
const personPrototype ={
    introduce : function(){
        return `안녕하세요. 제 이름은 ${this.name}입니다.`;
    }
}

const person1 = Object.create(personPrototype); // 새 객체를 생성하고 프로토타입을 지정함
person1.name = '길동이';

const person2 = Object.create(personPrototype);
person2.name = '둘리';

person1.introduce(); // 안녕하세요 제 이름은 길동이입니다.
person2.introduce(); // 안녕하세요 제 이름은 둘리입니다.
```
    - 이렇게 한 객체에서 다른 객체의 기능을 가져와 사용하는 것을 프로토타입 상속(Prototype inheritance)이라고 한다.
    - `personPrototype`은 `person1`의 프로토타입이다.
    - `person1` 객체는 `personPrototype` 객체를 상속받았다
1. `new` => 126번 줄


## 프로토타입 읽기
- `Object.getPrototypeOf`
- 위 함수를 이용하여 프로토타입을 읽을 수 있다
```js
const parent = {
    familyName : '심'
}
const child = Object.create(parent);

Object.getPrototypeOf(child) === parent; //true
// 현재 parent는 child의 프로토타입이다.
// child 객체는 parent 객체를 상속받았다.
```

## 프로토타입 쓰기
- `Object.setPrototypeOf`
- 위 함수를 이용하여 프로토타입을 쓸 수 있다.
    - (객체가 생성된 이후에 프로토타입을 변경하는 작업은 굉장히 느리므로 지양)
```js
// 읽는 함수의 코드에 이어서
const newParent ={
    familyName:'송'
}
Object.setPrototypeOf(child, newParent) // child 객체의 프로토타입을 newParent로 한다.
Object.getPrototypeOf(child) === parent; //false
// 현재 child 객체는 newParent를 상속받고있다.
```
- 객체 리터럴을 통해 생성된 객체의 프로토타입에는 자동으로 `Object.prototype`이 지정된다.
```js
const obj = {};
Object.getPrototypeOf(obj) === Object.prototype; // true
```
## 프로토타입 확인
- `.isPrototypeOf()`
- 위의 함수를 이용하여 어떤 객체가 다른 객체의 프로토타입 체인에 존재하는지 확인할 수 있다.
- `obj1.isPrototypeOf(obj3)`

## 프로토타입 체인 Prototype Chain
- JS 엔진은 프로토타입 객체의 속성까지 확인한다.
- 프로토타입 객체의 프로토타입 객체의 프로토타입 객체의 ......
- 이렇게 계속 이어져있는 프로토타입의 연쇄를 프로토타입 체인이라고 한다.
- 프로토타입 체인의 깊이가 너무 깊으면 속성의 읽기 속도에 영향을 미치므로 주의해야한다.
- 프로토타입 체인을 따라가다보면 언젠가는 `null`을 만나게 된다. 이 때에 확인하는 과정이 끝이난다.


## 속성 가리기 Property Shadowing
```js
const parent = {
    prop : 1
}
const child = {
    prop : 2
}

Object.setPrototypeOf(child, parent); // `child`의 프로토타입을 `parent`로 재설정한다.
child.prop; // 2
```
- 같은 이름의 속성이 있어도 프로토타입 체인의 상위에 있는 속성이 하위에 있는 속성에 의해 가려진다.
- 나중에 선언된 내용이 출력된다.

## 프로토타입을 간접적으로 변경하는 것은 불가능
```js
const parent = {
    prop : '^^'
}
const child = Object.create(parent); // parent를 child의 프로토타입으로 설정

// 프로토타입 객체의 속성을 간접적으로 삭제하는 것은 불가능하다.
delete child.prop;
parent.prop // '^^'

// 프로토타입 객체의 속성을 간접적으로 변경하는 것은 불가능하다.
child.prop = 'ㅠㅠ'
parent.prop // '^^'
child.prop // 'ㅠㅠ'
```
- 어떤 객체의 속성을 변경하거나 속성을 삭제하는 작업은 그 객체의 프로토타입에 아무런 영향을 미치지 않는다.


# 생성자 Constructor
- `new` 키워드를 이용하여 객체를 생성할 수 있다.
```js
const obj = new Object();

typeof Object; // 'function'
```
- `Object`는 함수이다.
- `new` 키워드로 만든 객체는 함수이다.
- `new` 키워드와 함께 사용하는 함수를 `생성자`라고 한다.

## 생성자 정의
- JS에는 `Object` 뿐만 아니라 내장된 많은 생성자들이 있고 프로그래머가 직접 생성자를 만들 수도 있다.
```js
// 생성자 정의
function Person(name){
    this.name = name;
}

// 생성자를 통한 객체 생성
const person1 = new Person('길동');

person1.name // '길동'
Person.name // 'name'
```
- 위에서 `function` 이라는 구문을 통해 `Person`이라는 생성자를 정의하고, 생성자 안에서는 `this` 키워드를 사용해서 새로 만들어질 객체의 속성을 지정해 주었다.
- `new` 키워드를 사용해서 객체를 생성하는 순간에 생성자 안에 있는 코드가 실행되어 객체의 속성이 지정되는 것이다.
- 생성자의 이름은 대문자로 시작하게끔 하는것이 관례.

## 인스턴스 Instance
- 생성자를 통해 생성된 객체를 그 생성자의 인스턴스라고 한다.
- ` const person1 = new Person('길동'); ` : `person1`이 `Person`의 인스턴스이다.
- `instanceof` 연산자를 이용해서 객체가 특정 생성자의 인스턴스가 맞는지를 확인할 수 있다.
```js
person1 instanceof Person; //true
```
- 객체 리터럴을 통해 생성된 객체는 `Object`의 인스턴스 이다
```js
const obj = {};
obj instanceof Object; // true
```

## 생성자와 프로토타입
- 생성자를 통해 만들어낸 객체의 프로토타입에는  생성자의 `prototype` 속성에 저장되어있는 객체가 자동으로 지정된다

```js
Object.getPrototypeOf(person1) === Person.prototype; //true
```
