---
title: Object Constructor - 생성자로 객체 만들기
date: 2019-05-27 21:18:13
tags: [new, constructor, object]
categories:
  - Programming
  - Javascript
---
객체 생성자(Object Constructor)는 **비슷한 객체를 무수히** 만들어낼 수 있다.

_cf. 객체 리터럴로 객체를 생성할 수도 있다. var dog = { name: '메시', breed:'푸들', weight: '6kg'}_

## 객체 생성자 만들기

```js
function Dog(name, breed, weight) {
  //객체 생성자 특징 1. a function, 2.name with Upper Case
  this.name = name; //3. 'this' Keywords
  this.breed = breed;
  this.weight = weight;
  //4. return nothing
}
```

## 객체 생성자 특징

1. 객체 생성자는 함수이다.
2. 생성자 함수명은 일반적으로 대문자로 시작한다.
3. `this` 키워드를 사용한다.
4. 생성자 함수는 아무것도 반환하지 않는다.

<!-- more -->

## 생성자 사용법과 new 연산자(new Operator)

```js
function Dog(name, breed, weight) {
  this.name = name;
  this.breed = breed;
  this.weight = weight;
} //객체 생성자 만들기

var messi = new Dog("메시", "푸들", "6kg");
//객체 생성자 사용하여 객체 만들기 - 아래 작동방식의 예시
var fido = new Dog("피도", "진돗개", "30kg");
var ace = new Dog("에이스", "닥스훈트", "1kg");
```

### 작동방식 🔥

1. `new` 연산자가 새로운 **빈 객체**를 만든다.
2. `new`는 _`this`가 방금 새롭게 만든 빈 객체를 가리키도록_ 만든다.
3. 객체 생성자 Dog함수를 호출하고, '메시', '푸들', '6kg'을 인자로 전달한다.
4. 함수의 블럭이 호출되고, 아까 만든 빈 객체의 속성에 값들이 할당된다.
5. messi가 그 객체의 참조 변수가 된다.

## 예시로 만들어진 객체들

```js
messi 객체
{
	name: '메시',
	breed: '푸들',
	weight: '6kg'
}

fido 객체
{
	name: '피도',
	breed: '진돗개',
	weight: '30kg'
}

ace 객체
{
	name: '에이스',
	breed: '닥스훈트',
	weight: '1kg'
}
```

<참고>

- HeadFirst Javascript
