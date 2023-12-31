---
title: JavaScript에서 특정 시간으로 날짜 객체 만들기
date: 2023-08-08 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 자바스크립트시간
---

## 문제 상황

웹 개발을 하다보면 JavaScript로 날짜와 시간을 다루는 경우가 많습니다. 특히, 주어진 날짜에 특정 시간을 설정해야 하는 상황도 자주 발생합니다. 그럼 어떻게 주어진 날짜에 원하는 시간을 설정할 수 있을까요?

## 해결 방법

### 방법 1: setHours 메서드 사용

JavaScript의 `Date` 객체는 여러 가지 메서드를 제공하는데, 그 중 `setHours` 메서드를 사용하면 특정 시간을 설정할 수 있습니다.

```javascript
let date = new Date();  // 현재 날짜와 시간을 가져옴
date.setHours(14, 30, 0, 0);  // 시간을 14시 30분 0초 0밀리초로 설정
```

### 방법 2: Date 생성자에 파라미터 전달

`Date` 객체를 처음부터 원하는 날짜와 시간으로 생성할 수도 있습니다. 이때 생성자에 파라미터를 여러 개 전달하면 됩니다.

```javascript
let date = new Date(2023, 9, 1, 14, 30, 0, 0);  // 2023년 10월 1일 14시 30분 0초 0밀리초
```

## 주의 사항

* JavaScript의 월은 0부터 시작합니다. 즉, 1월은 0, 12월은 11입니다.
* `setHours` 메서드는 원래 객체를 수정합니다. 새로운 객체를 만들고 싶다면 복사를 해야 합니다.
* 시간은 24시간 형식을 사용합니다.

## 오류 이름

`TypeError`

## 결론

JavaScript에서 날짜와 시간을 다루는 것은 꽤 간단합니다. `setHours` 메서드나 `Date` 생성자를 사용하여 특정 시간을 쉽게 설정할 수 있습니다. 이 정보를 활용하여 다양한 웹 애플리케이션에서 유용하게 사용할 수 있을 것입니다.