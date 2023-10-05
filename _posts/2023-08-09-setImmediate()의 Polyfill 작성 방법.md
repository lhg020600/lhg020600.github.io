---
title: setImmediate()의 Polyfill 작성 방법
date: 2023-08-09 20:00:00 +0900
categories:
  - JavaScript
tags:
  - setImmediate
---

## setImmediate()가 필요한 이유

`setImmediate()` 함수는 비동기 코드를 실행할 때 유용하며, 이 함수는 현재 이벤트 루프가 끝나자마자 실행됩니다. 즉, 콜백 함수를 가능한 한 빠르게, 다른 코드나 이벤트를 방해하지 않으면서 실행하려는 경우 이 함수를 사용할 수 있습니다. 그러나 이 함수는 모든 브라우저에서 지원되지 않습니다. 그래서 polyfill이 필요한 상황이 발생할 수 있습니다. 

## Polyfill이 무엇인지 간단히 설명

Polyfill이란 브라우저에서 지원되지 않는 기능을 자바스크립트로 구현하여 지원할 수 있게 만드는 코드 조각을 의미합니다.

## setImmediate()의 Polyfill 작성 코드 예시

아래는 `setImmediate()` 함수에 대한 간단한 polyfill 코드입니다. 

```javascript
if (!window.setImmediate) {
  window.setImmediate = function(cb) {
    return setTimeout(cb, 0);
  };
}
```

이 코드는 `window` 객체에 `setImmediate` 함수가 없는 경우, `setTimeout()` 함수를 이용해 0밀리초의 지연을 가지고 콜백 함수를 실행하도록 합니다. 

## 주의사항

위의 polyfill 예제는 가장 간단한 형태입니다. 실제 구현에서는 더 많은 로직이 필요할 수 있습니다. 예를 들어, 인자를 전달해야 하는 경우, 즉시 실행이 필요한 경우 등 다양한 조건을 고려해야 합니다. 

## Error Name

만약 이 polyfill 코드가 제대로 작동하지 않는다면, 주로 `TypeError` 또는 `ReferenceError`와 같은 에러가 발생할 수 있습니다. 

## 마치며

`setImmediate()`의 polyfill을 작성하는 것은 비교적 간단하지만, 실제 상황에 맞게 코드를 수정해야 할 수도 있습니다. 위의 코드 예시와 설명을 참고하여 필요한 로직을 추가하시기 바랍니다.