---
title: 웹페이지에서 폼 제출시 Ctrl Click 또는 Shift Click으로 현재 페이지 새로고침하기
date: 2023-08-21 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 웹페이지폼
---

## 문제 상황

웹 개발을 하다보면, 사용자가 폼을 제출할 때 특별한 키를 함께 누르는 경우에 대응해야 하는 상황이 있습니다. 예를 들어, 사용자가 Ctrl+Click 또는 Shift+Click을 이용해 폼을 제출하면, 원치 않게 새 창이나 새 탭에서 페이지가 열릴 수 있습니다. 이럴 때 현재 페이지에서 자동으로 새로고침을 하고 싶다면 어떻게 해야 할까요?

## 해결 방법: JavaScript 이벤트 리스너 활용

JavaScript를 이용하면 이 문제를 쉽게 해결할 수 있습니다. 이벤트 리스너(event listener)를 설정해 특정 키가 눌렸는지 감지하고, 그에 따라 원하는 동작을 실행시킬 수 있습니다.

```javascript
document.addEventListener('keydown', function(event) {
  if (event.ctrlKey || event.shiftKey) {
    event.preventDefault(); // 기본 동작 중지
    location.reload(); // 현재 페이지 새로고침
  }
});
```

위의 코드는 'keydown' 이벤트를 감지하여 Ctrl 키 또는 Shift 키가 눌린 경우에 현재 페이지를 새로고침합니다. `event.preventDefault();`는 브라우저의 기본 동작을 중지시킵니다. 이후 `location.reload();` 코드가 실행되어 현재 페이지가 새로고침됩니다.

## 주의사항

이 방법을 사용할 때 주의해야 할 점은 모든 Ctrl+Click 또는 Shift+Click 동작에 대해 페이지가 새로고침될 것이라는 것입니다. 이로 인해 사용자가 원하는 다른 동작이 방해받을 수 있으니, 이를 적용할 부분을 신중하게 선택해야 합니다.

## 결론

JavaScript의 이벤트 리스너를 활용하면, 사용자가 폼을 Ctrl+Click 또는 Shift+Click으로 제출했을 때 현재 페이지를 새로고침하는 기능을 쉽게 구현할 수 있습니다. 하지만 이 기능을 적용할 때는 사용자 경험에 영향을 미칠 수 있으므로 주의가 필요합니다.