# React Suspense

## 개요

React Suspense는 **비동기 컴포넌트를 렌더링할 때의 로딩 상태를 처리**하는 기능입니다. `React.lazy`와 함께 사용하면 코드 분할(Code Splitting), 데이터 패칭 등의 비동기 작업 중 사용자에게 자연스러운 UX를 제공할 수 있습니다.

초기에는 코드 스플리팅만 지원했지만, React 18부터는 `Concurrent Features`와 `Suspense for Data Fetching` 기능까지 제공되며, 더 넓은 비동기 처리 범위로 확장되었습니다.

---

## 📌 기본 사용법: 코드 스플리팅

React.lazy와 Suspense를 사용해 동적으로 컴포넌트를 불러올 수 있습니다.

```tsx
// LazyComponent.tsx
export default function LazyComponent() {
  return <div>지연 로딩된 컴포넌트입니다!</div>;
}
```

```tsx
// App.tsx
import React, { Suspense, lazy } from "react";

const LazyComponent = lazy(() => import("./LazyComponent"));

function App() {
  return (
    <div>
      <h1>React Suspense Demo</h1>
      <Suspense fallback={<div>로딩 중...</div>}>
        <LazyComponent />
      </Suspense>
    </div>
  );
}
```

### ✅ 핵심 포인트

- `fallback` 속성: 로딩 중 보여줄 UI
- `lazy`는 `default export` 컴포넌트만 지원
- 주로 큰 컴포넌트/라우트에서 사용해 초기 번들 사이즈 축소

---

## 🔄 React 18에서의 Suspense for Data Fetching

React 18에서는 `startTransition`, `useDeferredValue`, `SuspenseList`, `use` API 등을 활용해 **데이터 패칭까지 Suspense로 다룰 수 있습니다.**

### 1. React 18 `use` API (experimental)

```tsx
// api.ts
export async function getData() {
  const res = await fetch("/api/data");
  return res.json();
}
```

```tsx
// DataComponent.tsx
import { use } from "react";
import { getData } from "./api";

const dataPromise = getData();

export default function DataComponent() {
  const data = use(dataPromise);
  return <div>데이터: {data.title}</div>;
}
```

```tsx
// App.tsx
import { Suspense } from "react";
import DataComponent from "./DataComponent";

function App() {
  return (
    <Suspense fallback={<p>데이터 불러오는 중...</p>}>
      <DataComponent />
    </Suspense>
  );
}
```

> 💡 `use()` 훅은 현재 React 서버 컴포넌트나 experimental 환경에서만 사용 가능

---

## 🔗 SuspenseList

`SuspenseList`를 사용하면 여러 Suspense 컴포넌트들의 로딩 순서를 제어할 수 있습니다.

```tsx
<SuspenseList revealOrder="forwards">
  <Suspense fallback={<Spinner />}>
    <ComponentA />
  </Suspense>
  <Suspense fallback={<Spinner />}>
    <ComponentB />
  </Suspense>
</SuspenseList>
```

- `revealOrder="forwards"`: 첫 번째가 준비될 때까지 기다렸다가 순차 렌더링
- `together`, `backwards`, `none` 등의 옵션 존재

---

## 📦 Suspense와 React Query

React Query와의 연동을 통해 Suspense를 데이터 패칭에 적극적으로 활용할 수 있습니다.

```tsx
const { data } = useQuery(["todos"], fetchTodos, { suspense: true });

<Suspense fallback={<Loading />}>
  <TodoList />
</Suspense>;
```

> ⚠️ 이 경우 `ErrorBoundary`도 함께 사용해야 안전합니다.

---

## 🧠 유의사항 및 베스트 프랙티스

### ✔️ Suspense는 반드시 fallback이 필요합니다

컴포넌트가 비동기 작업 중일 때 보여줄 UI를 `fallback`에 꼭 정의해야 합니다.

### ✔️ ErrorBoundary와 함께 사용하라

Suspense는 로딩은 다뤄도 에러는 다루지 않기 때문에, 별도로 오류 처리를 추가해야 합니다.

```tsx
class ErrorBoundary extends React.Component {
  state = { hasError: false };
  static getDerivedStateFromError() {
    return { hasError: true };
  }
  render() {
    if (this.state.hasError) return <p>문제가 발생했습니다.</p>;
    return this.props.children;
  }
}
```

### ✔️ Server Components와의 통합 (React 18)

- 서버에서 데이터를 패칭하고 Suspense로 감싸 렌더링 타이밍 제어 가능
- 성능 최적화에 유리

---

## 📚 결론

React Suspense는 비동기 UI 상태를 더욱 우아하게 처리할 수 있도록 도와주는 기능입니다. 기존에는 코드 분할 중심으로 사용했지만, 이제는 데이터 패칭, 서버 렌더링까지 지원 범위가 확장되었습니다.

실무에서 React 18의 `Suspense`, `SuspenseList`, `use`, `startTransition` 등을 적절히 조합해 사용하면 앱의 사용자 경험과 성능을 동시에 개선할 수 있습니다.

---

## 📎 참고 링크

- [React 공식문서 - Suspense](https://reactjs.org/docs/concurrent-mode-suspense.html)
- [React 18 Docs](https://react.dev/blog/2022/03/29/react-v18)
- [React Query - Suspense](https://tanstack.com/query/v4/docs/react/guides/suspense)
