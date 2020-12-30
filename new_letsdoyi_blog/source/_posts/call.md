---
title: "this 를 원하는 객체와 연결하기, call, apply, arguments"
tags:
  - arguments
  - call
  - apply
date: 2019-07-14 18:49:03
categories:
- Programming
- Javascript
---

```js
function.call(object);
```
의미: function이라는 함수가 실행될 때 그 안의 this가 object를 가리키도록 해

<!-- more -->

## Syntax

```js
function.call(object, argument1, argument2, arguments3 etc);
````
실행할함수.call(함수안의 this가 가리킬 객체, 실행할 함수에서 받아올 인자들, , , )
arguments들은 적는 것은 옵션사항이다.

```
function.apply(object, [arg1, arg2, arg3...]);
```
실행할 함수.apply(함수안의 this가 가리킬 객체, 실행할 함수에서 받아올 인자들의 집합)
arguments의 집합을 적는 것은 옵션사항이다.

```
function.arguments;
```
return 값은 function의 arguments 속성!은 an Array-like object 유사배열이다.
따라서 arguments속성을 배열의 속성들과 매서드를 모두 자유롭게 사용하고 싶다면, Array.from(arguments)를 사용하면된다. arguments를 배열로 바꿔주어야 한다.

```
Array.from(arguments)
```
의미: Array를 만들어라, 유사배열 arguments 로부터 온
return값은 arguments 유사배열의 각 요소를 요소로 하는 배열

<참고>
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call
