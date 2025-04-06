# React 상태 관리 (State Management)

## 1. 상태(State)란?

React에서 상태(state)는 컴포넌트의 동적인 데이터를 의미합니다. 사용자의 입력, 서버의 응답, 타이머 이벤트 등으로 인해 상태가 변경되며, 상태가 변경되면 컴포넌트는 자동으로 다시 렌더링됩니다.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>증가</button>
    </div>
  );
}
```

이 예시에서 `count`는 상태이며, 버튼 클릭에 따라 상태가 변경되고 컴포넌트가 재렌더링됩니다.

---

## 2. 상태 관리의 필요성

React는 기본적으로 단방향 데이터 흐름을 따르며, 상위 컴포넌트에서 하위 컴포넌트로 props를 통해 데이터를 전달합니다. 그러나 컴포넌트 간의 상호작용이 많아질수록 상태를 효율적으로 관리하는 것이 중요해집니다.

### 상태 관리가 필요한 상황 예시

- 여러 컴포넌트가 동일한 데이터를 공유해야 할 때
- 서버의 데이터를 가져와서 여러 곳에서 참조해야 할 때
- 상태 변경에 따른 부수 효과(side effect)가 많을 때

---

## 3. 상태 관리 방식

### ✅ 1. Local State

- 컴포넌트 내부에서만 사용하는 상태
- `useState`, `useReducer` 훅을 이용해 관리

```jsx
const [name, setName] = useState("");
```

### ✅ 2. Global State

- 여러 컴포넌트가 공유해야 하는 상태를 중앙에서 관리
- 전역 상태 관리를 위해 다양한 상태 관리 라이브러리 사용

### ✅ 3. Server State

- 외부 서버에서 데이터를 받아와 사용하는 상태
- 비동기 처리, 로딩 상태, 에러 처리 등 추가 고려사항 필요

### ✅ 4. URL State

- URL 쿼리 파라미터나 경로에 따라 동작이 바뀌는 경우
- React Router와 함께 상태처럼 관리 가능

---

## 4. 주요 상태 관리 도구

| 도구        | 특징                                   | 사용 예시                     |
| ----------- | -------------------------------------- | ----------------------------- |
| Context API | 기본 제공, props drilling 방지         | 사용자 정보, 테마 설정        |
| Redux       | 미들웨어, DevTools 지원, 강력한 생태계 | 대규모 앱, 복잡한 상태 관리   |
| MobX        | 반응형 상태 관리, 선언적 코드          | 빠른 프로토타입 제작, UI 상태 |
| Recoil      | React 전용, 파생 상태 관리 용이        | 상태 간 의존성이 복잡한 앱    |
| Zustand     | 작고 빠름, Hook 기반                   | 가볍고 단순한 상태 공유       |
| React Query | 서버 상태 전용, 캐싱, 리페칭 자동화    | 데이터 중심 앱, 대시보드 등   |

---

## 5. 상태 분리 전략

상태를 관리할 때는 상태의 **역할과 책임**을 구분하는 것이 중요합니다.

### 🎯 UI 상태 vs 비즈니스 상태

- **UI 상태**: 모달 열림 여부, 폼 입력값 등 UI에만 영향을 주는 상태
- **비즈니스 상태**: 사용자 정보, 인증 상태, 장바구니 등 전역적 의미의 상태

### 🎯 전역 vs 지역 상태 판단 기준

- 해당 상태가 여러 컴포넌트에서 공유되나요?
- 상태 변경이 다른 컴포넌트에 영향을 미치나요?
- 데이터를 서버에서 가져오나요, 내부에서 생성하나요?

```jsx
// 예시: React Query + Local State 혼합 사용
const [isOpen, setIsOpen] = useState(false);
const { data: user, isLoading } = useQuery(["user"], fetchUser);
```

---

## 6. 상태 최적화 전략

### 🔧 상태 최소화

- 꼭 필요한 데이터만 상태로 선언합니다.

### 🔧 상태 이동

- 상태는 그 상태를 가장 많이 사용하는 컴포넌트에 위치시킵니다.

### 🔧 렌더링 최적화

- `React.memo`, `useMemo`, `useCallback`을 활용하여 불필요한 렌더링 방지

```jsx
const MemoizedComponent = React.memo(function Component({ value }) {
  return <div>{value}</div>;
});
```

---

## 7. 결론 및 요약

React에서의 상태 관리는 단순히 `useState`만으로 끝나는 것이 아닙니다. 앱의 규모가 커질수록 상태를 분리하고, 적절한 위치에 배치하고, 필요한 도구를 사용하는 전략이 중요합니다.

- 로컬, 전역, 서버 상태를 구분하여 관리합니다.
- Context API는 간단한 전역 상태에 적합합니다.
- Redux, Recoil, Zustand 등은 복잡한 상태 관리에 효과적입니다.
- 서버 상태는 React Query 또는 SWR을 사용하면 효율적입니다.

> 적절한 도구와 설계를 통해 상태 관리를 잘하면 유지보수가 쉬운 안정적인 애플리케이션을 만들 수 있습니다. 🚀
