---
title: ActiveXObject와 GUID를 이용한 객체 생성 방법
date: 2023-08-16 20:00:00 +0900
categories:
  - JavaScript
tags:
  - ActiveXObject
---

## Stack Overflow의 질문 요약

질문자는 `ActiveXObject`를 GUID (Globally Unique Identifier)를 사용하여 생성하는 방법에 대한 지식을 얻고 싶어합니다. GUID는 전세계에서 고유한 식별자로, 프로그래밍에서 많이 사용됩니다.

## ActiveXObject란?

ActiveXObject는 Microsoft의 브라우저, Internet Explorer에서 사용되는 객체 모델입니다. 주로 웹 브라우저와 로컬 시스템 간의 상호 작용을 위해 사용됩니다. 

## GUID란?

GUID는 Globally Unique Identifier의 약어로, 고유한 값을 가지는 문자열입니다. 이 값은 전세계 어디에서도 중복되지 않는 고유한 값으로, 데이터베이스, 프로그래밍에서 고유한 키 값으로 사용됩니다.

## ActiveXObject 생성과 GUID

일반적으로 ActiveXObject는 프로그램의 이름을 사용하여 생성됩니다. 예를 들면, `new ActiveXObject("Excel.Application")` 같은 방식으로요. 그러나 GUID를 사용하여 ActiveXObject를 생성하는 것은 특별한 경우에만 사용됩니다. 

Stack Overflow에서 제시된 방법은 다음과 같습니다:

```javascript
var obj = new ActiveXObject("{6BF52A52-394A-11D3-B153-00C04F79FAA6}");
```

여기서 `{6BF52A52-394A-11D3-B153-00C04F79FAA6}`는 Windows Media Player의 GUID입니다.

## 주의사항

GUID를 사용하여 ActiveXObject를 생성하는 것은 권장되지 않습니다. 이 방법은 특별한 상황에서만 사용되어야 하며, 일반적인 경우에는 프로그램의 이름을 사용하는 것이 더 안전하고 이해하기 쉽습니다.

## 정리

ActiveXObject와 GUID를 결합하여 객체를 생성하는 방법은 가능하지만 권장되지 않습니다. 이는 특별한 상황에서만 사용되어야 하며, 일반적으로는 프로그램의 이름을 이용한 생성이 더욱 권장됩니다. 이러한 지침을 따르면 프로그래밍에서 발생할 수 있는 다양한 문제를 미리 예방할 수 있습니다.