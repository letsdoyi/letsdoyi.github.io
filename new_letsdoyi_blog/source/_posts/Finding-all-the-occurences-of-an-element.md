---
title: '원하는 요소 배열에서 모두 찾기'
date: 2019-05-03 23:49:11
tags:
  - indexOf()
  - Array
categories:
- Programming
- Javascript
---
```js
var indices = [];
var array = ['hi', 'b', 'hi', 'c', 'hi'];
var element = 'hi';
var idx = array.indexOf(element);

for(;idx !== -1;){
  indices.push(idx);
  idx = array.indexOf(element, idx + 1);
}

console.log(indices);//[0, 2, 4];
```

` arr.indexOf(searchElement, fromIndex)` fromIndex부분은 **fromIndex 부분부터** searchElement를 찾으라는 뜻이다. fromIndex가 음수라면, 배열의 처음부터 searchElement를 찾게 되고, fromIndex가 배열의 길이보다 크거나 같다면, -1이 반환된다.

<출처>
- https://developer.mozilla.org
