---
title: Prevent the previous event listener from triggering on a new click 문제 해결하기
date: 2023-09-21 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 자바스크립트에러
---

## 원인 파악
이 문제가 발생하는 주된 원인은 새로운 클릭 이벤트에 대해 이전의 이벤트 리스너가 여전히 활성화되어 있기 때문입니다. 이는 주로 이벤트 리스너를 추가하는 코드가 반복적으로 실행되는 경우에 발생합니다. 

## 해결 방법 1: removeEventListener 사용하기

이벤트 리스너를 추가하기 전에 `removeEventListener` 메소드를 사용하여 기존에 할당된 이벤트 리스너를 제거할 수 있습니다. 이렇게 하면 이전의 이벤트가 새로운 클릭에 영향을 미치지 않습니다.

```javascript
element.removeEventListener('click', functionName);
element.addEventListener('click', functionName);
```

## 해결 방법 2: once 옵션 활용하기

`addEventListener` 메소드에 `once` 옵션을 사용하면, 이벤트 리스너가 한 번만 실행됩니다. 즉, 이벤트가 발생하면 자동으로 리스너가 제거됩니다.

```javascript
element.addEventListener('click', functionName, { once: true });
```

## 해결 방법 3: 플래그 변수 사용하기

플래그 변수를 사용하여 이전 이벤트 리스너의 실행을 제어할 수 있습니다. 이렇게 하면 새로운 클릭에 이전 이벤트가 실행되지 않습니다.

```javascript
let isClicked = false;

function functionName() {
  if (!isClicked) {
    isClicked = true;
    // 이벤트 로직
  }
}
```

## 정리
이벤트 리스너 중복 실행 문제는 다양한 방법으로 해결할 수 있습니다. 필요에 따라 적절한 방법을 선택하여 이 문제를 해결할 수 있습니다. 이를 통해 사용자 경험을 향상시킬 수 있습니다.