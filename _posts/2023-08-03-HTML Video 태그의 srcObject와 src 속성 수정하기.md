---
title: HTML Video 태그의 srcObject와 src 속성 수정하기
date: 2023-08-03 20:00:00 +0900
categories:
  - JavaScript
tags:
  - srcObject
---

## HTML Video 태그 개요

HTML의 Video 태그는 웹 페이지에 비디오를 임베드하는 데 사용됩니다. 일반적으로 `src` 속성이나 `srcObject` 속성을 사용하여 비디오의 소스를 지정할 수 있습니다. 이러한 속성을 동적으로 변경하면, 웹 페이지에서 비디오 콘텐츠를 교체할 수 있습니다.

## src와 srcObject의 차이

`src`와 `srcObject` 속성은 비슷해 보이지만 다르게 작동합니다. `src`는 주로 비디오 파일의 URL을 지정하는 데 사용되며, `srcObject`는 미디어 스트림 객체(MediaStream)를 직접 연결할 때 사용됩니다. MediaStream 객체는 보통 웹캠이나 마이크 등의 미디어 디바이스로부터 데이터를 가져옵니다.

## JavaScript를 이용한 속성 변경

### src 속성 변경하기

`src` 속성은 문자열로 비디오 파일의 URL을 저장합니다. 이를 변경하는 것은 매우 간단합니다.

```javascript
var videoElement = document.getElementById("myVideo");
videoElement.src = "new_video.mp4";
```

### srcObject 속성 변경하기

`srcObject`는 조금 복잡합니다. 미디어 스트림 객체를 할당해야 합니다. 이는 보통 `getUserMedia` API를 통해 얻습니다.

```javascript
navigator.mediaDevices.getUserMedia({ video: true })
  .then(stream => {
    var videoElement = document.getElementById("myVideo");
    videoElement.srcObject = stream;
  })
  .catch(error => {
    console.error("Error: " + error.name);
  });
```

## 주의사항과 오류

두 속성을 동시에 사용하면, `srcObject`가 우선시 됩니다. 또한, `srcObject`를 사용할 때는 보안 문제를 유의해야 하며, HTTPS 프로토콜을 사용하는 것이 좋습니다.

오류가 발생할 경우, JavaScript 콘솔에서 다양한 에러 메시지를 확인할 수 있습니다. 대표적인 오류로는 `NotAllowedError`, `NotFoundError` 등이 있습니다.

## 결론

`src`와 `srcObject`는 HTML Video 태그에서 비디오 소스를 지정하는 방법 중 하나입니다. 이들을 JavaScript로 동적으로 관리하면 웹 페이지의 비디오 콘텐츠를 유연하게 제어할 수 있습니다.