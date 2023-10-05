---
title: 크롬 브라우저에서 setTimeout setInterval 이슈 해결하기
date: 2023-08-04 20:00:00 +0900
categories:
  - JavaScript
tags:
  - setTimeout
---

## 문제 상황: `setTimeout`과 `setInterval`의 동작 차이

크롬 브라우저에서는 백그라운드 탭에서 `setTimeout` 또는 `setInterval`을 사용할 때, 이 함수들이 예상대로 동작하지 않는 경우가 있습니다. 이러한 현상은 주로 탭이 비활성화 상태일 때 발생하며, 이로 인해 예상한 시간보다 더 늦게 코드가 실행되곤 합니다.

## 원인: 타이머 해제 알고리즘

크롬 브라우저는 리소스 사용을 최적화하기 위해 백그라운드 탭에서 실행되는 자바스크립트 코드의 속도를 제한합니다. 따라서 `setTimeout`과 `setInterval` 같은 타이머 함수들도 이 제한을 받게 됩니다.

## 해결 방안 1: Web Workers 사용

Web Workers는 백그라운드에서 실행되는 스크립트로, UI를 차단하지 않고 병렬로 작동합니다. Web Workers를 사용하면 크롬의 타이머 제한을 피할 수 있습니다.

```javascript
var myWorker = new Worker('worker.js');

myWorker.onmessage = function(e) {
  console.log('Message received from worker');
};
```

## 해결 방안 2: `requestAnimationFrame` 사용

`requestAnimationFrame`은 주로 애니메이션을 위해 사용되며, 브라우저의 다음 리페인트 때 실행됩니다. 이 함수는 백그라운드 탭에서도 더 정확하게 동작하는 특성이 있습니다.

```javascript
function myLoop() {
  // Your code here
  requestAnimationFrame(myLoop);
}

requestAnimationFrame(myLoop);
```

## 주의 사항

두 해결 방안 모두 특정 상황에서만 유용하므로, 필요에 따라 적절히 선택해야 합니다. 또한 Web Workers는 별도의 스레드에서 실행되므로 DOM에 접근할 수 없습니다.

## 정리

크롬 브라우저에서 백그라운드 탭에서 `setTimeout`과 `setInterval`이 제대로 동작하지 않는 문제는 다양한 해결 방법이 있습니다. Web Workers나 `requestAnimationFrame`을 사용해 이 문제를 극복할 수 있습니다.