---
title: "Prototype"
tags:
  - prototype
  - constructor
  - instance
  - dunder proto
  - job interview question
  - behavior delegation
toc: true
categories:
  - Programming
  - Javascript
date: 2019-06-03 16:51:59
---

자바스크립트의 Prototype 이란, 어떠한 객체가 만들어지기 위한 그 객체의 모태(원형)를 말한다. 자바스크립트의 모든 객체는 Object 객체의 프로토타입을 기반으로 확장 되었다.

Prototype은 크게 두가지 특징을 가지고 있다.

1. 생성자 (constructor) 와 쌍을 이룬다.
2. Instance 와 연결되어 있다. (Dunder proto와 prototype chain)

### 첫번째, 생성자 (constructor) 와 쌍을 이룬다.

마치 "부부"처럼, **생성자가 있으면 Prototype은 반드시 존재**한다. **생성자에는 아내인 Prototype에 대한 정보를 "기본적"으로 가지고 있다**. 그 정보(prototype의 reference)를 prototype 이라는 속성에 저장 한다. 반대로 아내 prototype도 남편의 정보(constructor의 reference)를 constructor라는 속성에 저장하고 있다.

아래 이미지에서 파란색 줄은 Object라는 생성자의 prototype 속성에 저장된 정보를, 노란색 줄은 생성자 아내(prototype)의 constructor 속성에 저장된 정보를 보여준다.

![](https://img.auctiva.com/imgdata/2/0/3/3/6/7/8/webimg/1031106316_o.png)

각각의 속성의 값들은 그 자체로 아내(prototype)와 남편(constructor)을 가리킨다.

<!-- more -->

```js
Object === Object.prototype.constructor;
//object를 '남편'이라고 한다면 object.prototype.constructor는 '남편의 아내의 남편'임으로 남편을 의미한다.
```

### 두번째, Instance 와 연결되어 있다.(Dunder proto와 prototype chain)

Instance - "An [object](https://developer.mozilla.org/en-US/docs/Glossary/object) created by a [constructor](https://developer.mozilla.org/en-US/docs/Glossary/constructor) is an instance of that constructor." **생성자함수에 의해 만들어진 객체를 인스턴스** 라고 한다. **생성자와 프로토타입의 자식** 이라고 생각할 수 있다.

```js
var hello = new Object();
// 'hello' 는 Object와 Object.prototype의 인스턴스이다.
```

**Dunder proto ( ** proto ** ) 는 인스턴스가 직접적으로 엄마인 prototype의 정보를 담아두는 속성**이다. 아래 그림에서 첫번째 주황색 줄을 보면, 생성자 함수로 hello 라는 (정확히는 hello 라는 참조를 갖는) 인스턴스를 만들었다. 그 후에 그 인스턴스 hello 를 출력 해보면, hello 객체 안에 ** proto ** 라는 속성이 들어있는 것을 볼 수 있다 - 세번째 주황색 줄. 그 속성 Dunder proto ( ** proto ** )의 값은 엄마의 정보(prototype의 reference)임을 알 수 있다 - 주황색 직사각형.

![](https://img.auctiva.com/imgdata/2/0/3/3/6/7/8/webimg/1031106562_o.png)

**Instance에 어떤 속성을 호출하면, Instance는 자신의 객체에서 "먼저" 속성값을 찾는다. 만약 속성값이 자신의 객체 안에 없다면, 연결된 Prototype (엄마, 생성자의 아내) 에서 속성값을 찾아 불러오고, 연결된 prototype에 찾는 속성이 없다면, Prototype의 Prototype(할머니)에서 속성값을 찾는다.** 이 일련의 현상을 **Prototype Chain** 이라고 한다. 프로로 타입 체인을 타고 올라가다 최고 조상인 Object.prototype 에서 멈추게 된다.

### Mitochondrial Inheritance VS Prototype Chain

_Object.prototype을 보니 Mitochondrial Eve가 떠오른다._ Prototype에서 "상속" 받았다는 표현을 쓰기도 하는 이유도 내가 Prototype Chain에 대해 알게 되면서 미토콘드리아 모계 "유전"을 떠올렸던 이유와 같을 것이다. 하지만, Prototype Chain 현상은 상속과 유전이라는 개념과는 매우 다르다. **Prototype 에서 속성값을 찾아 불러올 때 Instance는 그 속성값을 가지고 있지 않기 때문이다. Instance는 단지 Prototype에 속성들에 대한 접근 권한을 갖고 있다고 생각할 수 있고, 찾고 있는 속성에 접근하여 그 값을 불러오는 것이다.**

<img src="https://i.kinja-img.com/gawker-media/image/upload/s--RiC62xRp--/17enpavusehwzjpg.jpg" style="display: inline-block" width="250"> <img src="https://static.packt-cdn.com/products/9781849693127/graphics/3127_06_01.jpg" style="display: inline-block" width="400">

## Prototype Chain - 면접

### "class" or "Inheritance" VS "delegation" - you don't know js

속성값을 자기 객체로 가져와서 사용하는 것이 아니라는 점에서 **"상속"**이라는 표현보다 **"행동 위임" or "Behavior Delegation"**이라는 용어가 Prototype Chain 현상을 더 잘 표현한다.
