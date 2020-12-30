---
title: Why Typescript?
tags:
categories:
  - Programming
  - Paradigm
---

타입스크립트에 대해 정리해 보도록 하겠습니다.
타입스크립트는 "어떤 문제를 해결하기 위해" 등장한 언어이며, 타입스크립트를 "사용하는 이유" 에 대해 여러 블로그를 읽고 정리한 글 입니다.
_제 생각이 아닌 단순히 정리한 글이기 때문에 평어체를 쓰도록 하겠습니다._

<!-- more -->

# 1. 현존하는 자바스크립트의 문제

C#과 Java 같은 체계적이고 정제된 언어에서 사용하는 강한 타입 시스템은 높은 가독성과 코드 품질을 제공할 수 있고, 컴파일 환경에서 에러를 발생해 치명적인 오류를 쉽게 잡아낼 수 있다.

반면, 자바스크립트는 타입 시스템이 없는 동적 프로그래밍 언어로, 비교적 유연하게 개발할 수 있는 환경을 제공하지만, 간단한 오류조차 실제로 프로그래밍을 돌려 해당 코드가 실행되기 전에는 감지 할 수 없다.

타입스크립트는 현존하는 자바스크립트의 이러한 문제를 풀기 위해 등장했고, 그 수단으로 정적 타입 분석을 내세웠다.

# 2. 정적 타입 검사를 도입하고자 하는 움직임

자바스크립트의 문제점을 풀려고 했던 어떤 시도들이 있었을까?

- Typescaript
- Facebook의 Flow, https://flow.org/ - "Flow is a static type checker for Javascrpt."
- Elm, https://elm-lang.org/ - "A delightful language with no runtime exceptions."
- PureScript, https://www.purescript.org/, "A strongly-typed functional programming language that compiles to JavaScript."
- ReasonML, https://reasonml.github.io/ - "Reason lets you write simple, fast and quality type safe code while leveraging both the JavaScript & OCaml ecosystems."

# 3. 그렇다면 왜 타입스크립트 인가?

Flow, Elm, PureScript, ReasonML 등, 정적 타입 분석을 제공하는 여러 대체제가 있다. 이들 중 타입스크립트를 사용해야하는 이유는 무엇일까?

여러 대체제 중, Elm, PureScript, ReasonML 등의 언어는 자바스크립트 문법과 매우 이질적이였다. 따라서 3가지 큰 단점이 있었다.

- 기존 자바스크립트 코드베이스의 마이그레이션에 대한 비용이 커졌고 (전혀 다른 문법으로 프로젝트를 다시 작성해야 되기 때문)
- 기존 자바스크립트 개발자가 체감하는 학습 곡선이 가파라진다.
- 3rd party 자바스크립트 패키지의 사용이 어려워진다.

반면에 타입스크립트는 자바스크립트 코드를 이해하며 최신 ECMAScript 표준을 지원한다. 또한 위의 3가지 단점을 뒤집는 장점을 갖는다.

# 4. 타입스크립트의 그 자체로서의 장점

타입스크립트의 장점을 살펴보기 위해 타입스크립트가 무엇인지 살펴보자.

"TypeScript is a `typed` `superset` of JavaScript that compiles to plain JavaScript."

이 문장에서 주목해야할 포인트는 1. `typed` 와 2. `superset` 이다. 이 두 포인트 들에 주목해보자.

## 4-1. "Typed" 의미

- 정적 타입 시스템을 도입하여 컴파일 단계에서 오류를 포착할 수 있다.
- 명시적인 정적 타입지정은 개발자의 의도를 명확하게 코드로 기술 할 수 있어, 코드의 가독성을 높이고 예측할 수 있게 하며 디버깅을 쉽게 한다.

### 그렇다면 정적 타입 분석은 무엇을 의미하며, 어떤 장점을 제공 할까?

- Static Type System
  프로그램을 실행해 보지 않고도 런타임 이전에 타입 분석을 진행하는 방식이다. (<-> Dynamic Type System 실제로 실행될 때 타입분석)
  프로그램이 실제로 실행되기 전에 상당수의 오류를 잡아낼 수 있다. (실 사용자가 맞닥뜨리는 버그중 15%를 사전에 예방할 수 있다는 논문 결과 - http://earlbarr.com/publications/typestudy.pdf)
  > our central finding is that both static type systems find an important percentage of public bugs: both Flow 0.30 and TypeScript 2.0 successfully detect 15%!

## 4-2. "Superset" 의 의미

- 타입스크립트의 상위집합이다. 따라서 기존의 자바스크립트의 모든 문법을 포용한다.
- 타입스크립트는 추가적인 타이핑 없이 자바스크립트를 이해함으로 도입의 진입장벽이 낮아졌다.
- 자바스크립트 프로젝트에서 점진적인 마이그레이션 또한 지원한다.

# 5. 타입스크립트의 성공적인 생태계

타입스크립트는 코어 개발자, 컨트리뷰터, 지원도구 라이브러리, 개발자 커뮤니티들의 형성에 크게 성공하였다.

### 추가. 타입스크립트의 구성요소

1. 언어 명세
   타입스크립트가 어떤 의미를 가지로 있고 어떻게 동작해야하는 지 기술해둔 문서가 있다.
   https://www.notion.so/ts-84653d9d7d294884b3c1350b30bd92cb#9fd9ad0767fb4522976467f8d125d10d

2. 컴파일러
   타입스크립트의 코드를 입력으로 받아, 명세에 맞게 해석한 후 대되는 자바스크립트 코드를 출력으로 내보낸다.
   대표적인 컴파일러의 구성 요소들
   - Parser: 코드를 읽고 구문을 해석함
   - Type Checker: 타입 정보에 모순이 없는지 검사
   - Emitter: 브라우저가 실행 가능한 자바스크립트 파일을 뱉어냄

### Reference

- https://ahnheejong.gitbook.io/ts-for-jsdev/01-introducing-typescript/elements-of-typescript
- https://heropy.blog/2020/01/27/typescript/
- https://poiemaweb.com/typescript-introduction
- https://www.typescriptlang.org/
