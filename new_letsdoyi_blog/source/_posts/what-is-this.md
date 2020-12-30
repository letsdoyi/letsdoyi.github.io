---
title: "this란 무엇일까?"
date: 2020-03-24 11:46:10
tags: ['this', 'context', 'new', 'call', 'apply', 'bind']
categories:
  - Programming
  - Javascript
---

## "그래서, this가 뭔가요?"

"`this`는 해당함수를 어떤 방식으로 호출하느냐에 따라 결정 됩니다. blur blur blur..."
"그래서, this가 뭔가요?"

면접에서 `this`에 대해 한참을 설명하고 나서 들었던 질문입니다. 저는 `this`를 단순히 객체를 가리키는 것 이라고만 생각하고 있었습니다. 면접 후, `this`에 대해 좀더 자세히 공부하였고, 머릿속에 있던 자바스크립트의 개념들과 이것(여기서의 이것은?)을 연결하여 이해 할 수 있었습니다. 아래의 내용들은 제가 `this`에 대해서 공부하면서 함께 공부했던 내용들을 정리해놓은 것입니다. 주로 [ZeroCho 님의 블로그](https://www.zerocho.com/)를 보고 공부하였습니다.

<!-- more -->

---

## Execution Context (실행 컨텍스트)

실행 컨텍스트를 이해하면서 `this`를 자연스럽게 이해할 수 있었습니다.
`this`뿐 아니라 `Scope`, `Closer`, `Hoisting` 등 자바스크립트의 필수적인 개념들을 하나의 그림으로 이해할 수 있었습니다.

실행 컨텍스트는 코드가 실행되는 문맥이라고 생각할 수 있습니다. 우선, 실행 컨텍스트의 흐름을 이해해야 합니다.

- 처음 코드를 실행하면 모든 것을 관리하는 전역 컨텍스트가 생깁니다.
- 함수 호출 시 마다 컨택스트가 하나씩 생깁니다.
- 그 컨텍스트 안에 `변수객체`, `Scope Chain`, `this` 가 생성됩니다.
  `변수객체`는 함수의 인자인 `arguments`와 해당 스코프의 변수인 `variable`을 포함합니다.
- 컨텍스트 생성 후, 함수가 실행됩니다.
  이때 함수에서 사용되는 변수들은 먼저 변수 객체 안에서 그 값을 찾고 없다면 스코프체인을 따라 올라갑니다.
- 함수 실행이 종료되면 해당 컨텍스트는 사라집니다.
- 페이지가 종료되면 전역 컨텍스트는 사라집니다.

### 컨텍스트를 객체로 이해하기

이 코드에서 무엇이 console로 찍힐까요?

```
var object = 'chocolate';

function foo(subject) {
  console.log(subject + ' need(s) ' + object + '!');
}

function bar() {
  var object = 'masks';
  foo('We');
}

bar();
```

컨텍스트를 이용해 하나씩 설명해보겠습니다.

- 처음 코드 실행시, `전역 컨텍스트`가 생깁니다.

  ```
  '전역_컨텍스트': {
    변수객체: {
      arguments: null,
      variable: []
    },
    scopeChain: ['전역 변수객체'],
    this: window
  }
  ```

  여기서 `this`를 확인할 수 있고, 아래와 같은 규칙을 가집니다.

  - `this`는 따로 설정하지 않으면 기본적으로 window로 설정이 됩니다. (wow!🤭)
  - `new` 키워드나 `bind`를 통해서 `this`를 설정해 줄 수 있습니다. (wow!🤭)

  `this`에 대한 답을 얻었습니다. 예제에 대한 이어지는 설명은 다른 포스트에 정리하겠습니다.

<출처>
ZeroCho 님의 블로그: https://www.zerocho.com/category/JavaScript/post/5741d96d094da4986bc950a0

## this에 대한 총 정리

`this`에 대한 현상들과 함께 정리해 보겠습니다.
영어에서 'this'는 문맥(context)에 따라 가리키는 값이 달라집니다. 자바스크립트의 `this`도 마찬가지 입니다.

- `this`는 기본적으로 window 객체로 설정이 되어있습니다. (브라우저에서 코드가 실행된다면!)
  그래서 일반 호출 방식(예를 들어, foo())으로 함수를 호출하면 `this`는 window 가 됩니다.

- 하지만 점 호출 방식(예를 들어, messi.getAge())으로 함수를 호출하게 되면 `함수 컨텍스트`가 생성되고 `this`는 점의 앞부분 객체으로 설정됩니다.
  한마디로 문맥이 달라지게 되는 것입니다.

  이전에 다른 포스트에서 정리해놓았던 예제를 컨텍스트와 함께 설명해 보겠습니다.

  ```
  var age = 100;

  var messi = {
    age: 1,
    getAge: function getAge() {
      console.log(this.age);
    }
  }

  messi.getAge();
  ```

  `getAge 함수 컨텍스트`에 대해 위와 같은 방식으로 설명해 보겠습니다.

  ```
  'getAge_함수_컨텍스트': {
    변수객체: {
      arguments: null,
      variable: null
    },
    scopeChain: ['getAge 변수객체', '전역 변수객체'],
    this: messi
  }
  ```

  여기서 `this`가 messi 객체로 설정됩니다. 따라서 `this.age`의 console 값은 1이 찍히게 됩니다.


- `call`, `apply`, `bind` 를 이용해서 `this`와 원하는 객체를 연결시킬 수 있습니다.
`call`, `apply`, `bind`에 대해서는 [이전 포스트, this 를 원하는 객체와 연결하기, call, apply, argument](http://localhost:4000/2019/07/14/call/)에 정리해 놓았습니다.
  ```
  foo.call(messi, arg1, arg2, ...);
  foo.apply(messi, argsArray);
  foo.bind(messi, arg1, arg2, ...);
  ```

- `new` keyword를 이용해서 `this`를 설정할 수 있습니다.
`new` keyword에 대해서는 [이전 포스트, Object Constructor - 생성자로 객체 만들기](http://localhost:4000/2019/05/27/Object-Constructor/)에 정리해 놓았습니다.
```
function Dog() {
  var name = 'messi';
  this.age = 1;
}

var name = 'max';
var age = 15;

var obj = new Dog();
console.log(obj.age); //1
```

### 맺음말

자바스크립트의 기본 동작들에 대해 공부하면서, `this`에 대해 모호했던 개념들이 사라졌고, 다른 다양한 개념들도 정리될 수 있었습니다. 특히 `Closure`개념에 대해 다시금 깨닫게 되었습니다. 이것은(여기서의 이것은?) 다음번에 정리해 보려고 합니다.

<참고>
- https://www.zerocho.com/category/JavaScript/post/5741d96d094da4986bc950a0
- https://codeburst.io/all-about-this-and-new-keywords-in-javascript-38039f71780c

### 끄적끄적

정리해 보다, 정리해보다
둘다 맞는 표현이군요.

>'어디 한번 해보겠다는 거야?'와 같이, '대들어 맞겨루거나 싸우다'를 뜻하는 말인 '해보다'는 한 단어이므로 붙여 쓰는 것이 맞습니다. 한 단어 '해보다'의 쓰임이 아닌 경우, 본용언과 보조 용언의 결합으로 보아 '해 보다'로 띄어서 쓰는 것이 원칙입니다. 다만, 이때 '해 보다'는 한글 맞춤법 제47 항에 따라 '해보다'로 붙여 쓰는 것이 허용됩니다. 예를 들어, '이거 네가 한번 해 볼래?'와 같이 '해 볼래'를 띄어 쓰는 것이 원칙이며 '해볼래'로 붙여 쓰는 것도 허용됩니다.

<출처>
국립국어원: https://www.korean.go.kr/
