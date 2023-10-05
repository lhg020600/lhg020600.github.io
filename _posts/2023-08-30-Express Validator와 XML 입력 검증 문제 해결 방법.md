---
title: Express Validator와 XML 입력 검증 문제 해결 방법
date: 2023-08-30 20:00:00 +0900
categories:
  - JavaScript
tags:
  - Validator
---
# Express Validator와 XML 입력 검증 문제 해결 방법

## 오류의 원인: `Cannot read property 'field' of undefined`

이 문제가 발생하는 주요 이유는 Express Validator가 기본적으로 JSON 데이터를 처리하도록 설계되어 있기 때문입니다. 따라서, XML 데이터를 올바르게 인식하지 못하고, 이로 인해 필드를 찾지 못하는 경우가 있습니다. 

## XML을 JSON으로 변환하는 방법

XML 데이터를 처리하려면 먼저 XML을 JSON 형태로 변환할 필요가 있습니다. 여러 가지 라이브러리가 있지만, `xml2js`나 `fast-xml-parser` 등을 사용할 수 있습니다. 이러한 라이브러리를 사용하면 XML 데이터를 쉽게 JSON으로 변환할 수 있으며, 그 후에 Express Validator로 유효성 검사를 할 수 있습니다.

## Express Validator를 통한 유효성 검증

JSON으로 변환한 후에는, Express Validator의 `.check()` 메서드를 사용하여 필드를 검증합니다. 이렇게 하면 이전과 같은 오류가 발생하지 않을 것입니다.

```javascript
const { check } = require('express-validator');

app.post('/your-route', [
  check('yourField', 'Your field is required').not().isEmpty(),
  // 다른 유효성 검증 코드
], (req, res) => {
  // 로직 구현
});
```

## 주의사항

XML 데이터를 사용할 때는 항상 주의가 필요합니다. 왜냐하면 XML 데이터는 복잡한 구조를 가질 수 있고, 그로 인해 시스템이 취약해질 수 있기 때문입니다. 예를 들어, XXE (XML External Entity) 공격이 그러한 위험 중 하나입니다. 따라서, 안전하게 XML을 처리하는 로직을 구현해야 합니다.

## 결론

Express Validator가 XML을 기본적으로 지원하지 않기 때문에 XML을 JSON으로 변환한 후 유효성 검사를 해야 합니다. 이렇게 하면 `Cannot read property 'field' of undefined`와 같은 오류를 피할 수 있습니다.