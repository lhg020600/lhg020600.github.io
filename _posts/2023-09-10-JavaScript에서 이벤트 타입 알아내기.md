---
title: JavaScript에서 이벤트 타입 알아내기
date: 2023-09-10 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 이벤트타입
---

## 개요

JavaScript에서 이벤트 핸들러 내에서 이벤트의 이름이나 타입을 알고 싶을 때가 있습니다. 이런 정보는 이벤트에 따라 다르게 동작하는 함수를 만들 때 유용하게 사용될 수 있습니다. 이 글에서는 이러한 문제를 해결하는 방법에 대해 자세히 알아보겠습니다.

## 이벤트 객체 활용하기

JavaScript에서 이벤트를 처리할 때 이벤트 핸들러 함수에 전달되는 `event` 객체를 사용하면 현재 발생한 이벤트의 이름이나 타입을 알 수 있습니다. `event.type` 프로퍼티를 통해 이 정보를 가져올 수 있습니다.

```javascript
button.addEventListener('click', function(event) {
    console.log("이벤트 타입은: " + event.type); // "click"이 출력됩니다.
});
```

여기서 `event.type`은 이벤트의 이름을 문자열로 반환합니다. 이 경우에는 'click'이라는 문자열이 반환됩니다.

## jQuery에서의 활용

jQuery를 사용하고 있다면, `event` 객체에는 동일한 `type` 프로퍼티가 있습니다.

```javascript
$("#button").click(function(event) {
    console.log("이벤트 타입은: " + event.type); // "click"이 출력됩니다.
});
```

## 복수의 이벤트 처리하기

한 요소에 여러 이벤트를 등록하고 이벤트 타입에 따라 다르게 동작하게 하려면, 아래와 같이 코드를 작성할 수 있습니다.

```javascript
element.addEventListener('click focus', function(event) {
    if (event.type === 'click') {
        // 클릭 시 동작
    } else if (event.type === 'focus') {
        // 포커스 시 동작
    }
});
```

## 주의사항

`event.type`은 이벤트가 발생한 시점에서만 유효합니다. 따라서 이벤트 외부에서 이 값을 참조하려고 하면 `undefined`가 될 수 있으니 주의해야 합니다.

## 결론

이벤트의 타입을 알아내는 것은 복잡한 로직을 간단히 해결할 수 있는 방법 중 하나입니다. `event.type`을 활용하면 현재 발생한 이벤트가 무엇인지 쉽게 파악할 수 있습니다. 이를 통해 이벤트에 따라 다르게 동작하는 함수를 만들 수 있어, 코드의 유연성을 높일 수 있습니다.