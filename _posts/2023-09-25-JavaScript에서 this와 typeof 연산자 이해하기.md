---
title: JavaScript에서 this와 typeof 연산자 이해하기
date: 2023-09-25 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 자바스크립트this
---

## `this` 키워드의 동작 원리

JavaScript에서 `this`는 실행 문맥(context)에 따라 다르게 작동합니다. 일반적으로 `this`는 호출한 객체를 참조합니다. 그러나 함수가 어떻게 호출되었는지에 따라 `this`의 값이 달라질 수 있습니다. 예를 들어, 일반 함수에서 `this`는 전역 객체를 가리킵니다. 반면에 객체의 메소드에서 `this`는 해당 객체를 가리킵니다.

## `typeof` 연산자가 미할당 변수를 어떻게 인식하는가

`typeof` 연산자는 변수의 데이터 타입을 문자열로 반환합니다. JavaScript에서는 변수를 선언하고 값을 할당하지 않으면, `undefined`로 자동 초기화됩니다. 따라서 `typeof` 연산자는 미할당 변수에 대해서도 `undefined`를 반환합니다.

예시:

```javascript
let x;
console.log(typeof x); // Output: "undefined"
```

## StackOverflow 질문과의 연관성

StackOverflow의 질문에서 코드는 아래와 같습니다:

```javascript
var myObject = {
  myMethod: function() {
    console.log(this); // Output: myObject
    console.log(typeof this.myProperty); // Output: "undefined"
  },
  myProperty: 'I am a property!'
};
myObject.myMethod();
```

이 코드에서 `myMethod` 함수는 `myObject`를 호출하므로 `this`는 `myObject`를 가리킵니다. 그러나 `this.myProperty`의 값은 `myMethod`가 실행될 때까지 결정되지 않습니다. 따라서 `typeof this.myProperty`를 평가하면 JavaScript 엔진은 `myProperty`가 아직 값이 할당되지 않았기 때문에 "undefined"를 출력합니다.

## 결론

JavaScript에서 `this`와 `typeof`는 실행 문맥과 변수 할당 상태에 따라 동작합니다. 이해하기 어려운 부분이 있을 수 있지만, 이 두 키워드는 JavaScript의 기본 동작 원리를 이해하는 데 중요한 역할을 합니다. 따라서 이러한 기능을 정확하게 이해하고 사용하면, 더 효율적인 코드를 작성할 수 있습니다.