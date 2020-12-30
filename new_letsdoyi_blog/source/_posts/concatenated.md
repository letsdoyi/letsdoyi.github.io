---
title: "Concatenated, 반복 문자열 문제"
tags:
  - CleverSolution
  - Algorithm
  - if( )
  - index( )
  - Javascript
categories: Algorithm
date: 2019-05-03 20:39:33
toc: true
---

The string is called prime if it cannot be constructed by concatenating some (more than one) equal strings together. For example, "abac" is prime, but "xyxy" is not("xyxy"="xy"+"xy"). Given a string determine if it is prime or not.

<!-- more -->

Input/Output
[input] string s
string containing only lowercase English letters

[output] a boolean value

true if the string is prime, false otherwise

## 문제이해

전체 문자열이 "어떤 문자열로 '반복되어 연결되어 있지 않다면 true"를 반환하고, "반복되어 연결 되어있다면 false"를 반환하는 문제이다. 예를 들어, "abac"라는 문자열은 true를 반환하고, "xyxy"는 "xy"로 반복되어 연결 되어 있음으로 false를 반환한다.

## Clever 해결방법

이 문제에 대한 다른 사람들의 짧고 멋진 풀이법 두가지를 정리해 보고자 한다.

### 첫번째, 작은 문자열의 반복으로 이루어지지 않은 문자열의 관점에서 본 해결방법

```js
function primeString(s) {
  return (s + s).indexOf(s, 1) == s.length;
}
```

문자열을 2개를 연결시킨 후 그 문자열을 찾으면, 당연히 그 인덱스는 연결부분이 나오게 된다.
ex "1234567" + "1234567" = "**1234567** **1234567**
작은 문자열의 반복으로 이루어진 문자열은, 문자열이 2개를 연결시킨 문자열에 포함이 되는 모양을 볼 수 있다.
ex "123123"+"123123" = "123**123123**123123" or "123123**123123**123"

```js
배운점
1. indexOf( ) 메서드
- 문자열 전체도 검색 할 수 있다.
- indexOf( a, **number**) 쉼표다음 부분은 number 인덱스 부터 a를 검색하라는 의미이다.|
2. 스킬1 : 주어진 문자열을 **늘리는** 변형도 해볼 것
```

### 두번째, 작은 문자열의 반복으로 이루어진 문자열의 관점에서 본 해결방법이다.

```js
function primeString(s) {
  for (let i = 2; i <= s.length; i++) {
    if (s.slice(0, s.length / i).repeat(i) == s) return false;
  }
  return true;
}
```

"123123" + "123123" = "123**123123**123123" or "123123**123123**123"
전체 문자열을 특정조각으로 자른 뒤 그 조각은 반복한 값과 원래의 문자열을 비교한다.

```js
배운점
3. 스킬2 : 내가 **원하는 값을 만든 후**, 원래의 것과 비교
4. if 구문 statement가 한 줄일 경우, a block statement ({})를 쓰지 않아도 된다.
```

## 나의 해결방법

내가 생각한 문제 풀이법은 코드가 비효율적으로 길다. 문제를 빨리 풀어 레벨을 올리고 싶은 마음에 깊이 생각하지 않고 오류가 날 때마다 오류난 조건들을 if절로 커버하면서 풀었기 때문이다. 이제는 알고리즘 문제 해결 실력을 늘릴 수 있도록, 효율적 해결법에 대해 충분히 고민한 후, 코드작성을 해야겠다.

해결법
'전체 문자열 배열로 만든 후 배열을 두조각으로 나눠 a배열과 b배열을 비교하기'
이때 for문을 사용해서 a배열에 한 문자씩 넣고, a배열과 같은 길이 다음 인덱스 부터 그 길이만큼을 자른 후(b배열)
a.join값과 bjoin값을 비교한다
a.join값과 b.join값이 같다면, 다음 a길이만큼을 전체배열에서 잘라 비교하여, 마지막 배열까지 같은지 비교하였다.

전체 배열 abababababsakldfjaslkdfj
a배열 ab라면
b배열은 ab/ab/abababsakldfjaslkdfj, ab
