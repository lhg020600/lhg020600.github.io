---
title: ContentEditable의 모든 입력을 안정적으로 중단하는 방법
date: 2023-09-06 20:00:00 +0900
categories:
  - JavaScript
tags:
  - ContentEditable
---

## 문제 상황 및 오류 코드

스택오버플로우에는 'ContentEditable' 영역에서 모든 입력을 신뢰성 있게 중단하는 방법에 대한 여러 질문이 있습니다. 사용자는 `input`, `keydown`, `keypress` 같은 이벤트를 이용해서 이를 구현하려고 했으나 원하는 결과를 얻지 못했습니다. 특히 `event.preventDefault()` 함수를 사용하더라도 일부 입력은 여전히 발생하는 문제가 있습니다.

## 해결 전략

### 이벤트 버블링과 캡쳐링 이해하기

이벤트 버블링과 캡쳐링은 웹 페이지에서 이벤트가 어떻게 전파되는지를 설명하는 용어입니다. 이벤트 버블링은 이벤트가 자식 요소에서 부모 요소로 전파되는 것을 의미하고, 이벤트 캡쳐링은 그 반대입니다. 이 두 과정을 이해하면 원하는 이벤트만을 효과적으로 제어할 수 있습니다.

### addEventListener 사용하기

`addEventListener` 메서드를 이용하면 원하는 이벤트를 정밀하게 제어할 수 있습니다. 이 메서드는 세 번째 인자로 객체를 받을 수 있으며, 이 객체의 `capture` 속성을 `true`로 설정하면 이벤트 캡쳐링 단계에서 이벤트를 잡을 수 있습니다.

```javascript
document.querySelector("[contenteditable]").addEventListener("keydown", function(event) {
  event.preventDefault();
}, { capture: true });
```

### Input 이벤트에도 적용하기

`keydown` 이벤트만을 제어해서는 충분하지 않을 수 있습니다. 따라서 `input` 이벤트에 대해서도 같은 방식을 적용할 필요가 있습니다.

```javascript
document.querySelector("[contenteditable]").addEventListener("input", function(event) {
  event.preventDefault();
}, { capture: true });
```

## 주의 사항

이러한 방법은 대부분의 경우에서 잘 작동하지만, 브라우저나 운영체제, 입력 방식에 따라 예외가 있을 수 있습니다. 그러므로 꼼꼼한 테스트가 필요합니다.

## 마무리

ContentEditable의 모든 입력을 안정적으로 중단하는 것은 까다로울 수 있습니다. 그러나 이벤트 버블링과 캡쳐링을 이해하고, `addEventListener` 메서드를 올바르게 사용한다면 이 문제를 해결할 수 있습니다.