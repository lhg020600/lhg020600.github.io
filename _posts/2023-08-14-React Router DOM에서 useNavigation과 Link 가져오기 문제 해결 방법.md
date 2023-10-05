---
title: React Router DOM에서 useNavigation과 Link 가져오기 문제 해결 방법
date: 2023-08-14 20:00:00 +0900
categories:
  - JavaScript
tags:
  - useNavigation
---

## 문제 개요

이 글에서는 React Router DOM 라이브러리에서 `useNavigation` 혹은 `Link`를 가져오는 도중 발생하는 오류와 그 해결 방법에 대해 자세히 알아보겠습니다. 오류 이름은 `Module not found: Can't resolve 'react-router-dom'`입니다.

## 원인 파악

먼저, 이 오류가 나는 이유는 라이브러리가 올바르게 설치되지 않았거나, 잘못된 버전을 사용하고 있을 가능성이 높습니다. 또한, 패키지 관리자에 따라 문제가 발생할 수도 있으니, `npm` 또는 `yarn`에 문제가 없는지 확인하는 것이 중요합니다.

## 해결책 1: 라이브러리 재설치

가장 간단한 방법은 라이브러리를 재설치하는 것입니다. 이렇게 하면 일시적인 문제나 오류가 해결될 수 있습니다.

```bash
npm uninstall react-router-dom
npm install react-router-dom
```

## 해결책 2: 버전 확인

라이브러리의 버전이 올바른지 확인해보세요. 예를 들어, 문서에는 React Router DOM 버전 6을 사용하도록 되어 있지만, 실제로는 버전 5를 사용하고 있다면 문제가 발생할 수 있습니다.

## 해결책 3: 패키지 관리자 확인

`npm`과 `yarn`을 혼용해서 사용하면 이러한 문제가 발생할 수 있습니다. 한 가지 패키지 관리자만 사용하는 것이 좋습니다.

## 해결책 4: 경로 문제 해결

`useNavigation`은 특정 버전의 React Router DOM에서만 사용할 수 있습니다. 따라서 해당 함수가 실제로 라이브러리에 있는지 확인해야 합니다. `useNavigate`라는 이름으로 변경되었을 수도 있으니 확인이 필요합니다.

## 마무리

`Module not found: Can't resolve 'react-router-dom'` 오류는 다양한 원인으로 발생할 수 있습니다. 라이브러리 재설치, 버전 확인, 패키지 관리자 확인, 그리고 경로 문제 해결 등을 통해 이 문제를 해결할 수 있습니다. 이러한 방법들을 차례대로 시도해보면 문제를 해결할 수 있을 것입니다.