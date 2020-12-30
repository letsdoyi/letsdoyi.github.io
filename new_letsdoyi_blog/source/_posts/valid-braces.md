---
title: "Vaild braces - 괄호 짝찾기"
date: 2019-06-11 21:59:35
tags:
toc: true
categories:
- Algorithm
---

## 문제

괄호들로 이루어진 string을 입력받아서, 괄호들의 순서가 올바른지 판단해주는 함수를 완성해주세요. 괄호들은 ()와 {}와 [], 이렇게 총 3가지 종류가 있습니다. 괄호들은 자기와 짝이 맞는 괄호를 만나야만 합니다.

<!-- more -->

다음의 예를 봐주세요.

```js
"(){}[]"   =>  True
"([{}])"   =>  True
"(}"       =>  False
"[(])"     =>  False
"[({})](]" =>  False

@param {string} braces
@return {boolean}
```
<!-- more -->

## 문제 이해

괄호들이 이루어진 string을 입력받아서, 그 소, 중, 대괄호가 모두 유효한지 검사하는 알고리즘을 짜는 문제이다.

## 해결 방법1

여러가지 괄호 string의 경우를 생각 해보고, 귀납적으로 해결방법을 구상했다.

그 중 괄호가 유효할 수 있는 최소한의 조건을 추렸다.

1. "(){}[]" => True, 전체 괄호 string의 길이가 짝수이어야 한다.
2. "(}" => False, 특정괄호의 개수와 그 짝 괄호의 개수가 같아야 한다.
3. "[(])" => False, 짝괄호 사이의 공간 값이 짝수이어야 한다.

## 코드 구현1

```js
function validBraces(braces) {
  var checking;
  var arrS1 = [];
  var arrS2 = [];
  var arrM1 = [];
  var arrM2 = [];
  var arrL1 = [];
  var arrL2 = [];

  //1. 전체 braces길이가 짝수 인지 확인
  if (braces.length % 2 === 0) {
    function check(brace, saveArr) {
      while (position1 !== -1) {
        var position1 = braces.indexOf(brace, position1 + 1);
        if (position1 !== -1) saveArr.push(position1); //brace 가 들어있는 인덱스로 배열 만들기
      }
    }

    check("(", arrS1);
    check(")", arrS2);
    check("{", arrM1);
    check("}", arrM2);
    check("[", arrL1);
    check("]", arrL2);

    //2. 특정 괄호와 그 짝괄호의 개수가 같은지 확인하기
    function checkArrLength(array1, array2) {
      if (array1.length === array2.length) {
        return 1;
      } else {
        return 0;
      }
    }
    var cAlS = checkArrLength(arrS1, arrS2);
    var cAlM = checkArrLength(arrM1, arrM2);
    var cAlL = checkArrLength(arrL1, arrL2);

    //3. 짝괄호 사이의 공간 값이 짝수인지 확인
    function difference(Arr1, Arr2) {
      if (Arr1.length === 0) {
        checking = 0;
        return checking;
      } else {
        for (var i = 0; i < Arr1.length; i++) {
          if ((Arr2[i] - Arr1[i]) % 2 === 1) {
            checking = 0;
            return checking;
          } else {
            checking = -1;
            return checking;
          }
        }
      }
    }

    var S = difference(arrS1, arrS2);
    var M = difference(arrM1, arrM2);
    var L = difference(arrL1, arrL2);

    //2,3 을 모두 만족할 경우 true
    if (S + M + L === 0 && cAlS * cAlM * cAlL === 1) {
      return true;
    } else return false;
  }
  return false;
}
```

## 결과 분석1

```js
validBraces("}}]]))}])"); //false
validBraces("())({}}{()][]["); //false
validBraces("{}{[{}}]({})[]"); //true
validBraces("{}{[{}}]({})[]"); //true
validBraces("[(])"); //false
```

## 통과1

## 해결 방법 2 - stack 자료구조 이용, Last-In First-Out(마지막으로 들어가서 먼저 나온다)

1. str(괄호들로 이루어진 문자열)을 왼쪽부터 오른쪽까지 탐색한다.
2. 왼쪽이 닫힌 '( or [ or {' 괄호를 만나면 배열에 쌓는다.
3. 오른쪽이 닫힌 ') or ] or }' 괄호를 만나면 배열의 마지막 요소와 매칭되는지 비교한다.
4. 매칭이 되면 배열의 마지막 요소를 지운다. 그렇지 않다면, 탐색을 계속한다.
5. 탐색이 끝난 후, 배열에 남은 요소가 있다면 'false'를, 남은 요소가 없다면 'true'를 return 한다.

```js
function matchingBrackets(str) {
  var checkArr = [];
  for (var i = 0; i < str.length; i++) {
    if (str[i] === "(" || str[i] === "[" || str[i] === "{") {
      checkArr.push(str[i]);
    } else {
      if (
        (checkArr[checkArr.length - 1] === "(" && str[i] === ")") ||
        (checkArr[checkArr.length - 1] === "[" && str[i] === "]") ||
        (checkArr[checkArr.length - 1] === "{" && str[i] === "}")
      ) {
        checkArr.pop();
      }
    }
  }
  if (checkArr.length === 0) {
    return true;
  } else {
    return false;
  }
}

matchingBrackets("(){{()[]}}[(){}]"); // true
matchingBrackets("[(){[{}]}([)[]]]"); // false
```
