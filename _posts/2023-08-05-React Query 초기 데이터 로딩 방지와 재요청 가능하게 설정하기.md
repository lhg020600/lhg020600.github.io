---
title: React Query 초기 데이터 로딩 방지와 재요청 가능하게 설정하기
date: 2023-08-05 20:00:00 +0900
categories:
  - JavaScript
tags:
  - ReactQuery
---

## 문제 상황 설명

React Query를 사용할 때 초기에 데이터를 불러오지 않도록 설정하고, 추후에 재요청을 할 수 있도록 하는 방법이 필요하다. StackOverflow에서 이에 관한 질문이 있었으며, 이 문제를 해결하기 위한 방법을 자세하게 설명하겠습니다.

## 'enabled' 옵션 활용

React Query의 `useQuery`나 `useMutation` 훅에는 `enabled`라는 옵션이 있다. 이 `enabled` 옵션을 `false`로 설정하면 초기 데이터를 불러오지 않게 됩니다. 이후에 `true`로 변경하면 데이터를 다시 불러올 수 있다.

```javascript
const { data, refetch } = useQuery("queryKey", fetchFunction, {
  enabled: false
});

// 나중에 데이터를 불러오려면
refetch();
```

## Custom Hook을 통한 제어

'enabled' 옵션만으로 부족하다면, custom hook을 만들어 제어할 수도 있다. 예를 들어, `useState`를 사용하여 `enabled` 상태를 관리하는 custom hook을 만들 수 있다.

```javascript
function useCustomQuery() {
  const [enabled, setEnabled] = useState(false);
  const queryInfo = useQuery("queryKey", fetchFunction, { enabled });

  const fetchData = () => {
    setEnabled(true);
  };

  return { ...queryInfo, fetchData };
}
```

## 재요청과 Refetch 메서드

`refetch` 메서드를 사용하면, 데이터를 강제로 다시 불러올 수 있다. 이는 `enabled` 옵션이 `false`인 상태에서도 가능하다. 이 메서드는 React Query의 기본 기능 중 하나로, 실시간 데이터 업데이트나 사용자의 액션에 따른 데이터 재로딩을 가능하게 한다.

## 주의사항: Error Code

이 모든 설정을 할 때 에러가 발생하면, `Error Fetching Data` 같은 에러 메시지가 출력될 수 있다. 이러한 상황에서는 React Query의 문서나 에러 로그를 꼼꼼히 확인하는 것이 중요하다.

## 정리

React Query에서 초기 데이터 로딩을 방지하고 재요청을 가능하게 하려면, `enabled` 옵션과 `refetch` 메서드를 적절히 활용하면 됩니다. 더 나아가 custom hook을 통해 더 세밀한 제어도 가능하다. 이러한 기능들은 데이터 관리를 효율적으로 하고, 사용자 경험을 향상시키는 데 크게 도움이 된다.