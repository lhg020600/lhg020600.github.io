---
title: setImmediate 폴리필의 구현
date: 2023-08-02 20:00:00 +0900
categories:
  - JavaScript
tags:
  - setImmediate
---

## 무엇이 문제인가요?

JavaScript 환경에서 `setImmediate` 함수는 코드의 다음 라인을 실행하기 전에 비동기 코드를 실행합니다. 그러나 이 함수는 모든 브라우저에서 지원되지 않습니다. 오류 메시지는 대개 `setImmediate is not defined`입니다.

## 폴리필이란 무엇인가요?

폴리필은 어떤 기능이 원래 존재하지 않을 때, 그 기능을 사용자가 직접 만들어 넣는 것을 의미합니다. 즉, 브라우저에서 지원하지 않는 함수나 메소드를 우리가 직접 만들어 넣는 것입니다.

## `setImmediate` 폴리필 만들기

`setImmediate` 함수를 모든 브라우저에서 작동하게 하려면 폴리필을 사용할 수 있습니다. 아래는 간단한 `setImmediate` 폴리필의 예입니다.

```javascript
if (typeof setImmediate === 'undefined') {
  window.setImmediate = function(callback) {
    return setTimeout(callback, 0);
  };
}
```

이 코드 조각은 `setImmediate` 함수가 존재하지 않을 경우 `setTimeout` 함수를 이용해 `setImmediate`를 흉내냅니다. 여기서 `setTimeout(callback, 0)`는 `callback` 함수를 가능한 빨리 실행하라는 의미입니다.

## 주의사항

이 폴리필은 완벽하지 않습니다. `setTimeout`을 사용하면 실제로 0 밀리초 후에 실행되지 않을 수 있습니다. 그러나 대부분의 경우에는 이 간단한 폴리필로도 충분할 것입니다.

## 결론

폴리필은 브라우저에서 지원하지 않는 기능을 구현하는 데 유용합니다. `setImmediate` 함수는 모든 브라우저에서 지원되지 않기 때문에, 위에서 제시한 폴리필을 사용하여 이 함수를 대체할 수 있습니다. 이렇게 하면 코드의 호환성을 높일 수 있습니다.