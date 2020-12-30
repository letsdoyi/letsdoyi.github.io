---
title: "홀수번 나타나는 정수 찾기"
Categories: Algorithm
date: 2019-05-08 00:51:29
---
주어진 배열에서, 홀수 번 나타나는 정수를 찾아주세요. 단, 홀수 번 나타나는 정수는 항상 한개뿐입니다. 예를들어, [1, 1, 1, 1, 10] 에서 1은 4번 나타나고, 10은 1번 나타나므로, 홀수 번 나타나는 정수는 10 입니다.

<!-- more -->

## 문제 이해

주어진 배열에는 숫자들이 요소로 들어있고, 그 숫자 중 홀수번 나타나는 정수를 찾는 문제이다.

## 해결 방법

첫번째 요소를 찾을 정수로 설정하고, 원래 배열에서 삭제하고, 다른 배열 b에 넣는다. 원래 배열에서 그 정수를 찾고 원래 배열에서는 삭제, b 배열에 넣는다. b 배열의 길이가 홀수인지 검토하고 홀수이면 반환한다.

## 코드 구현

```js
function findOddInt(array) {
  for (var i = 0; i < array.length; ) {
    var arr = [];
    var a = array[i]; //찾을 정수 설정
    arr.push(a); //arr에 찾을 정수 넣기
    array.shift(); //찾을 정수 배열에서 삭제
    for (var j = 0; j < array.length; ) {
      var b = array.indexOf(a); //배열에서 찾은 정수의 인덱스
      if (b !== -1) {
        arr.push(a); //동일한 정수로 이루어진 새로운 배열 설정
        array.splice(b, 1);
      } else {
        j = array.length;
      }
    }
    if (arr.length % 2 === 1) {
      return a;
    }
  }
}
```

## 결과 분석

```js
"test case 1",
  findOddInt([20, 1, -1, 2, -2, 3, 3, 5, 5, 1, 2, 4, 20, 4, -1, -2, 5]); // 5;
"test case 2", findOddInt([9]); // 9;
"test case 3", findOddInt([1, 1, 1, 1, 1, 1, 3, 3, 3]); //3;
"text case 4", findOddInt([1, 1, -1, -1, -1, 7, 7, 9, 9, 11, 11]); // -1;
```
