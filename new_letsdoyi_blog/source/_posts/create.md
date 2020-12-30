---
title: "객체를 생성자 함수처럼 사용하기, Object.create(obj)"
date: 2019-07-14 19:44:43
tags:
categories:
  - Programming
  - Javascript
---

```js
Object.create(obj);
```

obj을 프로토타입으로 가질 객체를 생성하시오
return 값은, 명시된 객체를 프로토 타입으로 가지고, 명시된 속성들을 가지는 새로운 객체

<!-- more -->

## Syntax

```js
Object.create(obj, propertiesObject);
```

Ojbect.create(프로토타입이 될 대상, 속성들의 세부사항들을 설정할 수 있는 객체)

## 참고 - propertiesObject (Optional parameter) Use Example

propertiesObject : It is optional parameter. It specifies the enumerable properties to be added to the newly created object.

<img src= "https://img.auctiva.com/imgdata/2/0/3/3/6/7/8/webimg/1033305686_o.png">
