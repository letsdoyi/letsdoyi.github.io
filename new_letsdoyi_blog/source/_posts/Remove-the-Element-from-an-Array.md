---
title: "배열 특정 요소 삭제"
date: 2019-04-30 16:28:37
tags:
  - splice()
  - slice()
  - Array
  - Delete
  - 오답노트
categories:
- Programming
- Javascript
---

코딩문제를 풀때, 특정 요소를 삭제하는 방법은 자주 사용된다. 아래는 **배열의 특정 요소 삭제 방법**과 내가 자주 **실수하는 포인트**들을 정리하였다. 다음은 **배열의 특정 요소 삭제 방법** 이다.

```javascript
배열이름.splice(인덱스, 1);
```

간단한 사용 예시

```javascript
var array = [1, 2, "ipad", 3, 4, 5];
var apple = array.splice(2, 1);
//array = [1, 2, 3, 4, 5]
//apple = ['ipad'], apple은 배열, array 타입이 된다
```

**실수하는 포인트**

> 주의사항
>
> 1. slice가 아닌 _splice_
> 2. 문자열에서는 사용이 불가능하다
> 3. splice는 기존 배열또한 변형이 일어나며, slice는 기존배열에 변화를 주지 않는다 (2019.5.2 update)

---_참고 Object의 속성을 지우는 메서드는 delete이다_

```javascript
var object = { Brand: "Samsung", ModelNumber: "2098d0dkd0" };
delete object.ModelNumber; //delete_객체명.속성명
//object = {Brand: 'Samsung'}
```
