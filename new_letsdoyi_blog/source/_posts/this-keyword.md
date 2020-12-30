---
title: "this keyword"
tags:
  - this
  - javascript
  - job interview question
  - 오답노트
date: 2019-06-03 15:14:35
categories:
  - Programming
  - Javascript
---

`this`가 객체를 가리킨다 하지만, 어떤 객체를 가리키는지는 `this`를 사용하는 해당 함수를 **"어떤 방식으로 호출하느냐"** 에 따라 결정된다.

<!-- more -->

```js
var name = "bow-wow";
var obj = {
  name: "ken",
  log: function() {
    console.log(this.name);
  }
};

obj.log(); // 'ken'

var fn = obj.log;
fn(); // 'bow-wow'
```

`this` 를 사용하는 해당 함수를 호출하는 방식에는 4가지가 있다.

## 1. Regular function call - 일반 함수 실행 방식

### 1-1. in non-strict mode

non-strict mode 에서 일반 함수 실행방식으로 `this` 를 사용한 함수를 호출했을 경우에 `this` 를 global object를 가리킨다.

```js
var name = "ken";

function foo() {
  console.log(this.name); // 'this' === global object (브라우저상에선 window 객체)
}

foo();
```

### 1-2. in strict mode (찾아보고 공부하기)

```js
"use strict";

var name = "ken";

function foo() {
  console.log(this.name); // 'this' === undefined
}

foo();
```

## 2. Dot Notation - 점 호출 방식

Dot notation 방식으로 `this` 를 사용한 함수를 호출했을 경우에 `this` 는 점 앞부분의 객체를 가리킨다.

```js
var age = 100;

var ken = {
  age: 35,
  foo: function foo() {
    console.log(this.age);
  }
};

ken.foo();
```

`ken.foo()` 가 Dot notation방식으로 실행되었음으로 `this.age` 의 `this` 는 ken 객체를 가리킨다. 따라서 `console.log` 값은 35가 나온다.

## 3. Explicit binding - 분명하게 `this`를 지정하는 방식

`Function.prototype.call`, `Function.prototype.bind`, `Function.prototype.apply`

### 3-1. call, apply

```js
var age = 100;
function foo() {
  console.log(this.age);
}
var ken = {
  age: 35,
  log: foo
};

foo.call(ken);
//foo 함수는 실행되고, `this`는 첫번째 인자 'ken'으로 지정된다.
```

```js
var age = 100;

function foo(a, b, c) {
  console.log(this.age);
  console.log(arguments);
}

var ken = {
  age: 35
};

foo.call(ken, 1, 2, 3, 4, 5, 6, 7, 8, 9); //35
foo.apply(ken, [1, 2, 3, 4, 5]); //35
```

### !! call과 apply 차이점은 면접 질문으로 자주 출제

```js
function.call(thisArg, arg1, arg2, ...) //thisArg는 필수요소
function.apply(thisArg, [argsArray]) //thisArg는 필수요소
```

`call`과 `apply`는 모두 this 값을 명시해주는 인자를 첫 번째 인자로 가지며 `return 값`도 this 가 지정된 함수를 호출하는 것으로 동일하다. 하지만, 이 둘의 차이점은 `call`은 "많은 인자"를 가질 수 있지만, `apply`는 "최대 2개의 인자"를 갖을 수 있고 "두 번째 인자는 배열"이여야 한다는 것이다.

### 3-2. bind

공부 중/

## 4. ['new' keyword](https://letsdoyi.github.io/2019/05/27/Object-Constructor/) 를 사용해서 실행한 함수

```js
function Person() {
  // this = {};
  this.name = "ken";
  // this = { name: 'ken' };

  // return this;
}

var ken = new Person();
console.log(ken);
```

`new` 연산자를 사용하면 빈 객체가 생기고, `this` 는 이 객체를 가리킨다.

## 틀린 예제 정리

## 예제1.

```js
var age = 100;
const something = {
  age: 1,
  speak: function() {
    console.log(this.age); // ?
  }
};
const butler = {
  age: 10,
  serve: function(cb) {
    cb();
  }
};
butler.serve(something.speak);
```

### 1-1. 정답

`butler.serve` 에서 `something.speak` 를 일반함수 호출방식으로 `cd()` 호출하고 있음으로 `this` 는 global object 를 가리키므로 답은 100 이다.

### 1-2. 나의 오답 이유

내가 헷갈렸던 부분은 `butler.seve` 의 인자 부분에 대한 해석이었다. `something.speak` 를 Dot Notation 방식으로 호출하려 한다면 `something.speak()` 가 올바르다. `something.speak` 는 속성에 대한 값을 나타낸다.

## 예제2.

```js
function programmer() {
  this.isSmart = false;
  this.upgrade = function(version) {
    this.isSmart = !!version;
    work();
  };
}

function work() {
  if (this.isSmart) {
    window.alert("I can do my work! I am smart!"); // ?
  }
}

var programmer = new programmer();
// THINK: What should happen?
programmer.upgrade(1.1);
```

### 2-1. 정답

`work` 함수안의 `this` 가 어떤 객체를 가리키고 있는 지 묻는 문제이다. `work()` 는 일반함수 호출방식으로 실행되었음으로 `work` 함수안의 `this` 는 global object를 가리킨다. 글로벌 객체에 `isSmart` 라는 속성은 정의되지 않았음으로, `window.alert` 는 실행되지 않는다.

1. `programmer.upgrade`의 키 값인 함수가 '1.1'를 인자를 갖고 실행된다.
2. `upgrade` 함수안의 `this` 는 `programmer` 를 가리킨다.
3. `programmer` 의 속성 `isSmart` 에 `!!1.1` 인 `true` 를 할당한다. (`!!version` 은 값을 불리언값으로 바꿔주는 역할)
4. `work` 함수를 일반호출 방식으로 실행한다.
5. `work` 함수안의 `this`는 글로벌 객체를 가리킴으로 `if` 조건문을 만족 하지않아 `alert` 메서드는 실행되지 않는다.
