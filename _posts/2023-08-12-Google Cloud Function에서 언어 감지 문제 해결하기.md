---
title: Google Cloud Function에서 언어 감지 문제 해결하기
date: 2023-08-12 20:00:00 +0900
categories:
  - JavaScript
tags:
  - GoogleCloud
---

## 문제 상황: 언어가 항상 'en'으로만 인식됨

Google Cloud Function을 사용하여 언어를 감지하는 작업을 수행하는 중, 언어가 항상 'en' (영어)으로만 인식되는 문제가 발생했다고 합니다. 이 문제를 해결하기 위해 여러 방법을 시도했지만, 성공하지 못했습니다. 이러한 상황을 겪고 있다면 아래의 정보를 참고하여 문제를 해결해보세요.

## 원인 분석: 코드의 미묘한 문제점
StackOverflow 질문에서 공개된 코드를 분석한 결과, `detectLanguage` 함수의 반환값이 'en'으로 고정되어 있는 것을 확인할 수 있었습니다. 그 이유는 Google Cloud Function의 비동기(asynchronous) 작업과 관련이 있을 가능성이 높습니다. 비동기란 여러 작업이 동시에 수행되는 것을 의미합니다.

## 해결 방법: Promise와 Async/Await 사용하기

비동기 문제를 해결하기 위해선 `Promise`나 `async/await` 문법을 사용할 수 있습니다. 이러한 키워드들은 자바스크립트에서 비동기 작업을 다루기 위한 방법입니다.

### Promise 사용 예시

```javascript
exports.detectLanguage = functions.https.onRequest((req, res) => {
  const textToDetect = req.query.text;
  client
    .detect(textToDetect)
    .then(results => {
      const detections = results[0].language;
      res.status(200).send(detections);
    })
    .catch(err => {
      console.error('ERROR:', err);
      res.status(500).send('Error');
    });
});
```

### Async/Await 사용 예시

```javascript
exports.detectLanguage = functions.https.onRequest(async (req, res) => {
  try {
    const textToDetect = req.query.text;
    const results = await client.detect(textToDetect);
    const detections = results[0].language;
    res.status(200).send(detections);
  } catch (err) {
    console.error('ERROR:', err);
    res.status(500).send('Error');
  }
});
```

## 마무리: 코드 수정으로 문제 해결
위의 예시 코드를 참고하여 Google Cloud Function 내의 `detectLanguage` 함수를 수정하면 언어 감지 문제가 해결될 가능성이 높습니다. 이러한 방식으로 비동기 문제를 극복하고, 원하는 언어 코드를 정확히 감지할 수 있을 것입니다.