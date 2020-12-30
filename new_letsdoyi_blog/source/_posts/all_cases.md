---
title: "m개 중 n개를 선택하여 만들 수 있는 모든 경우의 수"
date: 2019-05-22 19:54:35
tags:
categories: Algorithm
---

## 이 알고리즘을 생각하게 된 이유

알고리즘 문제를 풀다보면, 배열의 요소들 중에서 몇 개를 선택하여 배열을 만드는 알로리즘을 짤 수 있다면 문제를 효율적이고 쉽게 풀 수 있다는 생각이 들었고 이 알고리즘을 생각하게 되었다. 인터넷에서 n개를 선택하여 만들 수 있는 모든 경우의 수를 추출하는 알고리즘을 찾아보았지만, 잘 이해가 되지않아 직접 만들어보게 되었다.

<!-- more -->

## 컨셉

**이진법의 On, Off** 의 개념과 **수의 연속성**을 활용하였다. 배열의 요소들 중 포함한 요소를 1 (On) , 포함하지 않는 요소를 0 (Off) 이라고 표현한다. 예를 들어, 요소의 수가 3인 배열 [1, 2, 3] 중 2개의 요소로 만들 수 있는 배열은 이진법으로 110, 101, 011 이렇게 3가지 이다. 또한 이 방법은 수의 연속성을 활용하여 모든 경우를 빠짐없이 추출할 수 있다. 바로 앞 문장에서 나왔던 예시로 생각해보면, 1부터 7 (< 2의 3제곱수) 수를 이진법으로 표현한 뒤 1이 2번 들어가는 수를 추출하면 된다.

## 장점

이 방법은 배열의 요소의 수와 n의 수에 상관이 없고 빠짐없이 모든 경우의 수를 추출할 수 있다.

## 코드 구현 시 고려 사항들

1. 011은 처럼, 자리수를 모두 표현 해주기 위해 앞에 1을 붙인 수(2의 원하는 자리수 제곱)부터 범위를 시작한다. (이 의미없는 1은 나중에 제거한다)

2. 원하는 n만큼 1이 들어가 있다면 추출한다.

3. 1이 들어간 인덱스를 원래 배열의 인덱스로 사용해 원하는 요소가 들어간 배열을 만든다.

## 이 알고리즘을 활용해 푼 문제

John and Mary want to travel between a few towns A, B, C ... Mary has on a sheet of paper a list of distances between these towns. `ls = [50, 55, 57, 58, 60]`. John is tired of driving and he says to Mary that he doesn't want to drive more than `t = 174 miles` and he will visit only `3` towns.

Which distances, hence which towns, they will choose so that the sum of the distances is the biggest possible

- to please Mary and John- ?

Example:

With list `ls` and 3 towns to visit they can make a choice between: `[50,55,57],[50,55,58],[50,55,60],[50,57,58],[50,57,60],[50,58,60],[55,57,58],[55,57,60],[55,58,60],[57,58,60]`.

The sums of distances are then: `162, 163, 165, 165, 167, 168, 170, 172, 173, 175`.

The biggest possible sum taking a limit of `174` into account is then `173` and the distances of the `3` corresponding towns is `[55, 58, 60]`.

The function `chooseBestSum` (or `choose_best_sum` or ... depending on the language) will take as parameters `t` (maximum sum of distances, integer >= 0), `k` (number of towns to visit, k >= 1) and `ls` (list of distances, all distances are positive or null integers and this list has at least one element). The function returns the "best" sum ie the biggest possible sum of `k` distances less than or equal to the given limit `t`, if that sum exists, or otherwise nil, null, None, Nothing, depending on the language. With C++, C, Rust, Swift, Go, Kotlin return `-1`.

Examples:

```js
ts = [50, 55, 56, 57, 58]` `choose_best_sum(163, 3, ts) -> 163
xs = [50]` `choose_best_sum(163, 3, xs) -> nil (or null or ... or -1 (C++, C, Rust, Swift, Go)
ys = [91, 74, 73, 85, 73, 81, 87]` `choose_best_sum(230, 3, ys) -> 228
```

## 코드 구현

```js
function chooseBestSum(t, k, ls) {
  if (ls.length < k) return null;
  //seleted

  var bArr = new Array();
  var allCase = new Array();
  var sumArr = new Array();
  //FROM pow(2, ls.length)  TO Math.pow(2, ls.length + 1)

  for (
    var a = Math.pow(2, ls.length), i = 0;
    a < Math.pow(2, ls.length + 1);
    a++, i++
  ) {
    var b = a;
    for (bArr[i] = []; b >= 1; ) {
      bArr[i].unshift(b % 2);
      b = Math.floor(b / 2);
    }
  } //2D array by Binary Method

  for (var i = 0; i < bArr.length; i++) {
    bArr[i].shift();
    allCase[i] = new Array();
    for (var j = 0; j < bArr[i].length; j++) {
      if (bArr[i][j] === 1) {
        allCase[i].push(ls[j]);
      }
    }
  } //all cases array

  for (var i = 0; i < allCase.length; i++) {
    if (allCase[i].length === k) {
      var sum = 0;
      for (var j = 0; j < allCase[i].length; j++) {
        sum = sum + allCase[i][j];
      }
      sumArr.push(sum);
    }
  }

  sumArr.push(t);
  sumArr.sort(function(a, b) {
    return a - b;
  }); //sorted the array in ascending order

  if (sumArr[sumArr.indexOf(t) + 1] === t) {
    return t;
  } else if (sumArr[sumArr.indexOf(t) + 1] > t && sumArr.indexOf(t) === 0) {
    return null;
  } else {
    return sumArr[sumArr.indexOf(t) - 1];
  }
}
```
