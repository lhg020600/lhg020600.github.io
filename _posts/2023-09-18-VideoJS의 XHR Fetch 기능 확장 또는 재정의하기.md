---
title: VideoJS의 XHR Fetch 기능 확장 또는 재정의하기
date: 2023-09-18 20:00:00 +0900
categories:
  - JavaScript
tags:
  - VideoJS
---

## 개요

VideoJS에서 XHR 또는 Fetch를 사용하여 데이터를 가져오는 과정을 커스터마이징하고 싶다면 이 글이 도움이 될 것입니다. 여기서는 VideoJS 라이브러리 내에서 XHR 또는 Fetch 요청을 어떻게 수정하거나 확장할 수 있는지에 대한 상세한 방법을 설명합니다.

## 기존 방식의 한계

VideoJS는 웹에서 비디오를 플레이하는 데 자주 사용되는 자바스크립트 라이브러리입니다. 하지만 기본 설정대로는 네트워크 요청을 커스터마이즈하는 방법이 제한적입니다. 이러한 한계를 극복하기 위해서는 VideoJS의 내부 XHR 또는 Fetch 기능을 직접 수정해야 합니다.

## 방법 1: 비디오 소스를 설정할 때 옵션 추가하기

VideoJS의 `videojs` 함수를 호출할 때 `options` 객체에 XHR 또는 Fetch 관련 설정을 추가할 수 있습니다. 이 설정은 `html5` 키 안의 `hls` 객체에 위치해야 합니다.

```javascript
videojs("my_video", {
  html5: {
    hls: {
      overrideNative: true,
      xhrSetup: function(xhr, url) {
        xhr.setRequestHeader("Custom-Header", "value");
      }
    }
  }
});
```

## 방법 2: 미들웨어 활용하기

미들웨어(middleware)는 요청과 응답 사이에 위치하여 추가적인 로직을 수행할 수 있게 해줍니다. VideoJS 미들웨어를 사용하여 XHR 또는 Fetch 요청을 수정할 수 있습니다.

```javascript
videojs.use("*", function(player) {
  return {
    setSource(srcObj, next) {
      srcObj.src = modifyUrl(srcObj.src);
      next(null, srcObj);
    }
  };
});
```

## 코드 오류 해결: CORS 문제

CORS(Cross-Origin Resource Sharing, 교차 출처 리소스 공유)는 웹 보안과 관련된 문제입니다. 이 오류는 다른 도메인에서 리소스를 가져오려고 할 때 발생합니다. 이러한 문제를 해결하려면 서버 측에서 적절한 CORS 헤더를 설정해야 합니다.

## 마무리

VideoJS의 XHR/Fetch 기능을 커스터마이징하려면, 비디오 소스를 설정할 때 옵션을 추가하거나 미들웨어를 사용하는 두 가지 방법이 있습니다. 이러한 방법을 활용하면 네트워크 요청을 더 유연하게 관리할 수 있습니다.