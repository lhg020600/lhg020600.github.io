---
title: HTML 비디오의 srcObject 또는 src 속성 변경하기 in JS
date: 2023-08-15 20:00:00 +0900
categories:
  - JavaScript
tags:
  - srcObject
---

## 소개
웹 개발에서 비디오 컨텐츠는 상당히 중요한 요소 중 하나입니다. 이 글에서는 자바스크립트를 사용하여 HTML의 `<video>` 태그의 `srcObject` 또는 `src` 속성을 수정하는 방법에 대해 자세히 알아보겠습니다.

## src와 srcObject의 차이
`src`와 `srcObject`는 둘 다 HTML 비디오를 제어하기 위한 속성입니다. `src`는 일반적으로 비디오 파일의 URL을 저장하고, `srcObject`는 미디어 스트림 객체(MediaStream)을 저장합니다. `srcObject`는 주로 실시간 스트리밍에서 사용됩니다.

## src 속성 변경하기
자바스크립트에서 HTML 비디오의 `src` 속성을 변경하려면 다음과 같이 코드를 작성하면 됩니다.

```javascript
let videoElement = document.getElementById('myVideo');
videoElement.src = "new-video.mp4";
```

여기서 `new-video.mp4`는 새로운 비디오 파일의 경로입니다. 이렇게 하면 웹페이지에 있는 비디오가 새로운 비디오로 교체됩니다.

## srcObject 속성 변경하기
`srcObject` 속성을 변경하려면 미디어 스트림 객체가 필요합니다. 예를 들어 웹캠에서 비디오를 스트리밍하려면 다음과 같이 작성하면 됩니다.

```javascript
navigator.mediaDevices.getUserMedia({ video: true })
  .then(stream => {
    let videoElement = document.getElementById('myVideo');
    videoElement.srcObject = stream;
  })
  .catch(error => {
    console.error('MediaStream Error: ', error);
  });
```

`getUserMedia` 함수를 사용하여 웹캠의 미디어 스트림을 얻은 다음, `srcObject` 속성에 이 스트림을 할당합니다.

## 주의사항
두 속성을 동시에 사용하지 않아야 합니다. 둘 중 하나만 설정해야 올바르게 작동합니다. 동시에 설정하면 예기치 않은 동작이 발생할 수 있습니다.

## 결론
HTML `<video>` 태그의 `src` 또는 `srcObject` 속성 변경은 자바스크립트를 통해 간단하게 할 수 있습니다. `src`는 파일 경로를, `srcObject`는 미디어 스트림을 할당하여 비디오 소스를 변경할 수 있습니다. 두 속성 중 하나만 사용하는 것이 중요하며, 원하는 방식에 따라 적절한 속성을 선택해야 합니다.