---
title: Strapi에서 items.create 또는 items.update 후크에서 관계 설정하기
date: 2023-08-10 20:00:00 +0900
categories:
  - JavaScript
tags:
  - Strapi
---

## 문제 상황 정리

Strapi는 오픈 소스 헤드리스 CMS(Content Management System)로, API를 쉽게 생성하고 관리할 수 있습니다. 이 플랫폼에서는 데이터 관계를 설정하기 위한 다양한 방법이 있습니다. 하지만, `items.create` 또는 `items.update` 후크(hook)에서 이를 수행하려고 하면 어려움을 겪을 수 있습니다. 이 문제에 대한 해결 방법을 살펴보겠습니다.

## 해결 전략: Lifecycle 후크 사용하기

Strapi에서는 데이터 생성이나 업데이트를 진행할 때 특정 로직을 실행시킬 수 있도록 Lifecycle 후크를 제공합니다. 이는 `models` 폴더 내의 특정 모델 파일에서 설정할 수 있습니다.

예를 들어, `Article` 모델에 관련된 `Author`를 설정하려면 아래와 같이 코드를 작성할 수 있습니다.

```javascript
module.exports = {
  lifecycles: {
    async afterCreate(data, model) {
      // Author 관계 설정 로직
      await strapi.services.article.update({
        id: data.id,
        author: data.authorId,
      });
    },
    async afterUpdate(data, model) {
      // Author 관계 설정 로직
      await strapi.services.article.update({
        id: data.id,
        author: data.authorId,
      });
    },
  },
};
```

이 예시에서 `afterCreate`와 `afterUpdate`는 Lifecycle 후크입니다. 여기서 `strapi.services.article.update` 메서드를 이용하여 `Author`와 `Article`의 관계를 설정해 줍니다.

## 주의할 점: 무한 루프의 위험성

`afterCreate` 또는 `afterUpdate` 후크 내에서 다시 데이터를 업데이트하면 이 후크가 무한히 실행될 위험이 있습니다. 따라서 무한 루프를 피하기 위한 조건문이 필요합니다.

## 결론

Strapi에서 `items.create` 또는 `items.update` 후크에서 관계를 설정하는 것은 복잡할 수 있습니다. 그러나 Lifecycle 후크를 이용하면 이 문제를 깔끔하게 해결할 수 있습니다. 이 방법을 통해 Strapi에서 데이터 관계를 효율적으로 관리할 수 있을 것입니다.