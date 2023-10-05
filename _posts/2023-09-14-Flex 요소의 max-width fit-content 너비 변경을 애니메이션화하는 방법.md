---
title: Flex 요소의 max-width fit-content 너비 변경을 애니메이션화하는 방법
date: 2023-09-14 20:00:00 +0900
categories:
  - JavaScript
tags:
  - 플랙스요소
---

## 문제 상황 및 오류 메시지

개발자들은 때때로 CSS 애니메이션을 사용하여 웹사이트에 다이나믹한 요소를 추가하려고 합니다. 이와 관련하여 StackOverflow에 올라온 질문은, 플렉스박스(Flexbox)의 자식 요소에 `max-width: fit-content` 속성을 적용한 후, 이 요소의 너비를 애니메이션으로 변경하는 방법에 관한 것입니다.

오류 메시지는 특별히 없지만, 애니메이션 효과가 적용되지 않는 문제가 발생했습니다.

## `max-width: fit-content`와 애니메이션 문제점

`max-width: fit-content`는 요소의 최대 너비를 그 내용에 맞게 설정합니다. 하지만 이 속성은 CSS 애니메이션에 직접적으로는 적용되지 않습니다. 그래서 애니메이션을 사용하려면 다른 방법을 찾아야 합니다.

## 해결 방법 1: `max-width` 대신 `width` 사용

첫 번째 방법은 `max-width` 대신 `width` 속성을 애니메이션에 사용하는 것입니다. 이렇게 하면 애니메이션 효과를 쉽게 적용할 수 있습니다. 예를 들어, CSS에서 다음과 같이 설정할 수 있습니다.

```css
.element {
  transition: width 0.3s ease-in-out;
  width: 100px;
}

.element:hover {
  width: 200px;
}
```

## 해결 방법 2: 가상 요소 사용

두 번째 방법은 가상 요소(pseudo-element)를 사용하는 것입니다. 가상 요소를 만들어 그 위에 애니메이션 효과를 적용하면, 원래 요소에는 `max-width: fit-content`를 유지하면서 애니메이션 효과를 줄 수 있습니다.

```css
.element::before {
  content: "";
  transition: width 0.3s ease-in-out;
  width: 100px;
}

.element:hover::before {
  width: 200px;
}
```

## 결론

`max-width: fit-content` 속성은 애니메이션에 직접 적용되지 않기 때문에, `width` 속성을 이용하거나 가상 요소를 사용하는 방법 등을 고려해야 합니다. 이러한 방법들은 원하는 애니메이션 효과를 성공적으로 적용할 수 있게 해줍니다.