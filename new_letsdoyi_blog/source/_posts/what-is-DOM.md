---
title: "DOM, Document Object Model 이란?"
date: 2019-06-26 15:37:27
toc: true
tags: ["DOM", "node"]
categories:
  - Programming
  - DOM
# thumbnail: https://pbs.twimg.com/media/DPEdkAhX0AATdME?format=jpg&name=medium
---

HTML을 작성할 때에는 HTML 콘텐츠를 다른 HTML 콘텐츠 내에 캡슐화하여 문서를 작성한다.

```html
<html>
  <head></head>
  <html></html>
</html>
```

이를 통해 Tree로 표현 가능한 계층 구조가 만들어진다. 브라우저는 HTML 문서를 로딩할 때, 이 계층구조 (**Tree**)를 해석하여 마크업이 어떻게 캡슐화 되었는 지를 보여주는 **노드 개체(객체) 트리**를 생성한다.

<!-- more -->

```markdown
해석, 변환
HTML -------------> 노드 개체들의 Tree 구조인 DOM
by 브라우저
```

**DOM은 자바스크립트를 사용해 이 문서에 대한 스크립트 작성 (삭제, 추가, 바꾸기, 이벤트 처리, 수정)을 위한 프로그래밍 인터페이스를 제공**한다. _DOM은 원래 XML 문서를 위한 API였지만, HTML 문서에서도 사용 되도록 확장되었다._

## 노드 개체

**노드**의 사전적 의미는 '나무줄기의 마디' 혹은 '인체 관절 부근의 절' 이다.

<img src="https://4.bp.blogspot.com/-2iIKTPYvNDg/USPENU4y0TI/AAAAAAAAAJA/NIMV0Y8HExQ/s400/Nodes+and+Internodes.jpg" style="display: inline-block"  width="400"><img src="https://my.clevelandclinic.org/-/scassets/images/org/health/articles/8353-lymphedema.ashx" width="250" style="display:inline-block">

노드 개체 트리인 DOM을 하나의 나무라고 보면, 그 마디 각각을 **노드**라고 할 수 있다. 즉, **DOM Tree 구조에서 데이터의 상하위 계층을 나타내는 위치의 항목**이다.

<img style="display: block; transform: rotate(180deg)" src="http://www.ladybug.uconn.edu/FactSheets/pruning-terminolgy_2_3205640577.png" width="600">

## Node, 생성자 함수

통상적인 DOM Tree의 각 노드 개체는 **생성자 함수 Node** 로부터 속성과 메서드를 상속 받는다. _여기서 생성자 함수인 **Node** 는 노드 개체 와 구분하기 위해 영어로 표기하였다._

```js
					 		null
             |
             |.__proto__
             |
    	Object.prototype
             |
             |.__proto__
             |
      Node.prototype
             |
             |.__proto__
             |
     Element.prototype
             |
             |.__proto__
             |
 		HTMLElement.prototype
             |
             |.__proto__
             |
  	HTMLDivElement.prototype
```

다시 말하면, **모든 노드 유형은 Node로 부터 속성 및 메서드를 상속 (정확하게는 위임) 받으며**, 그 Node는 Object.prototype으로 부터 속성 및 메서드를 상속 (위임) 받는다.

```markdown
Object < Node < Element < HTMLElement
Object < Node < Attr
Object < Node < CharacterData < Text
Object < Node < CharacterData < comment
Object < Node < Document < HTMLDocument
Object < Node < Document < DocumentFragment
```

![text](https://docstore.mik.ua/orelly/webprog/jscript/figs/js4_1702.gif)

문서 내의 노드 유형에 따라 Node 개체를 확장한 하위 노드 개체 / 인터페이스 가 추가로 존재한다. 위의 목록은 가장 일반적인 노드 인터페이스에 대한 브라우저에서 구현된 상속 모델들이다.

## 노드 개체를 다루기 위한 Node 속성 및 메서드

- childNodes
- firstChild
- lastChild
- nextSibling
- **nodeName**
- **nodeType**
- nodeValue
- parentNode
- previousSibling
- appendChild()
- clondeNode()
- compareDocumentPosition()
- contains()
- hasChildNodes()
- insertBefore()
- isEqualNode()
- removeChild()
- replaceCild()

노드 인터페이스에서 제공되는 속성 및 메서드 외에, document, HTMLElement, HTML\*Element 인터페이스와 같은 하위 노드 인터페이스에서도 수많은 관련 속성 및 메서드가 제공된다.
