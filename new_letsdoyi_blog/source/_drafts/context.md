---
title: context
date: 2020-03-24 19:21:31
tags:
---

2. 함수가 호출될 때마다 각각의 컨텍스트가 생성됩니다.
   위 예제 코드에서 bar 함수가 먼저 호출 되었습니다. `bar_함수_컨텍스트`가 생성됩니다.

```
'bar_함수_컨텍스트': {
  변수객체: {
    arguments: [],
    variable: [{'object'}] //초기화 후에는 [{'object': 'masks'}]가 됩니다.
  },
  scopeChain: ['foo 변수객체', '전역 변수객체'],
  this: window
}
```

`변수객체`의 `variable`에 'object'가 들어간 것과 `scopeChain`에 `bar 변수객체`가 추가된 것을 볼 수 있습니다.

동일한 방식으로 `foo 함수 컨텍스트`도 생성됩니다.

```
'foo_함수_컨텍스트': {
  변수객체: {
    arguments: [{'subject' : 'We'}],
    variable: []
  },
  scopeChain: ['foo 변수객체', '전역 변수객체'],
  this: window
}


`변수객체`의 `arguments`에 'object'가, `scopeChain`에 `foo 변수객체`가 추가된 것을 볼 수 있습니다. `bar`함수안에서 `foo`함수가 실행 되더라도 스코프 체인을 타고 도달할 수 있는 변수객체에는 `bar변수객체`가 없습니다. 따라서 예제 코드의 답은 'We need(s) masks!'가 됩니다.
```
