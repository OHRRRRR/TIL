# React에서의 Lazy Loading과 Code Splitting

## 🧩 개요

React 애플리케이션이 커질수록 JavaScript 번들 사이즈도 커지고, 초기 로딩 속도는 느려집니다. 이를 해결하기 위한 대표적인 기법이 **Lazy Loading**과 **Code Splitting**입니다. 이 두 개념은 사용자 경험(UX)을 개선하고 성능을 최적화하는 데 필수적인 전략입니다.

---

## 🚀 Code Splitting이란?

**코드 스플리팅(Code Splitting)** 은 JavaScript 애플리케이션의 번들을 여러 개로 나누는 기술입니다. 기본적으로 Webpack 등의 번들러는 모든 코드 파일을 하나의 번들로 묶습니다. 하지만 `import()` 문법과 React의 `lazy()` 기능을 활용하면 필요한 시점에만 로딩되도록 코드를 분리할 수 있습니다.

### 📦 주요 이점

- 초기 로딩 시간 감소
- 필요한 페이지 혹은 컴포넌트만 로드
- 사용자 경험 개선

---

## 🕹️ React.lazy()와 Suspense

React는 `React.lazy()` 함수를 통해 동적 import로 컴포넌트를 로딩할 수 있습니다. `Suspense` 컴포넌트는 로딩 중 보여줄 UI를 설정합니다.

### ✅ 사용 예시

```tsx
import React, { Suspense } from "react";

const MyComponent = React.lazy(() => import("./MyComponent"));

function App() {
  return (
    <div>
      <Suspense fallback={<div>로딩 중...</div>}>
        <MyComponent />
      </Suspense>
    </div>
  );
}
```

> `fallback`은 해당 컴포넌트가 로드되기 전까지 보여줄 JSX입니다.

---

## 🧠 사용 시 주의사항

1. `React.lazy()`는 **default export**만 지원합니다.
2. `Suspense`는 반드시 lazy 로드된 컴포넌트를 **감싸야** 합니다.
3. 서버 사이드 렌더링(SSR) 환경에서는 별도 설정 없이 lazy를 사용할 수 없습니다.

---

## 📁 라우팅과 Lazy Loading

React Router v6 이상에서는 `lazy()`와 `Suspense`를 활용해 **페이지 단위 코드 분할**이 가능합니다.

### 예시: React Router v6

```tsx
import { createBrowserRouter, RouterProvider, Route } from "react-router-dom";
import { lazy, Suspense } from "react";

const Home = lazy(() => import("./pages/Home"));
const About = lazy(() => import("./pages/About"));

const router = createBrowserRouter([
  {
    path: "/",
    element: (
      <Suspense fallback={<p>로딩 중...</p>}>
        <Home />
      </Suspense>
    ),
  },
  {
    path: "/about",
    element: (
      <Suspense fallback={<p>로딩 중...</p>}>
        <About />
      </Suspense>
    ),
  },
]);

function App() {
  return <RouterProvider router={router} />;
}
```

---

## ⚒️ 번들 크기 시각화 도구

코드 분할 전략이 실제로 얼마나 성능에 영향을 주는지 확인하기 위해 다음 도구를 사용할 수 있습니다:

- [Webpack Bundle Analyzer](https://www.npmjs.com/package/webpack-bundle-analyzer)
- [Source Map Explorer](https://www.npmjs.com/package/source-map-explorer)

```bash
npm run build
npx source-map-explorer 'build/static/js/*.js'
```

---

## 🧩 dynamic import 활용 팁

동적 import는 단순히 lazy loading 외에도 조건부 렌더링, 사용자 권한 기반 로딩 등에 응용할 수 있습니다.

```tsx
function loadComponent(userRole) {
  if (userRole === "admin") {
    return import("./AdminDashboard");
  } else {
    return import("./UserDashboard");
  }
}
```

이처럼 동적 import는 React.lazy의 내부에서도 활용되며, 일반적인 JavaScript 동작과 동일하게 `.then()` 체이닝도 가능합니다.

---

## 🧵 Suspense for Data Fetching (React 18+)

React 18부터는 **데이터 패칭도 Suspense로 감쌀 수 있게** 되었습니다. 이는 `React Query`, `Relay`, `Next.js App Router` 등에서 점점 더 일반화되고 있습니다.

### 간단한 예시 (with React Query)

```tsx
import { Suspense } from "react";
import { useQuery } from "@tanstack/react-query";

function Post() {
  const { data } = useQuery({
    queryKey: ["post"],
    queryFn: fetchPost,
    suspense: true,
  });
  return <div>{data.title}</div>;
}

function App() {
  return (
    <Suspense fallback={<div>Loading post...</div>}>
      <Post />
    </Suspense>
  );
}
```

---

## 🧭 정리

| 개념              | 설명                                     |
| ----------------- | ---------------------------------------- |
| Code Splitting    | 번들을 작은 단위로 나눠 필요할 때 로드   |
| Lazy Loading      | 실제 사용하는 시점에만 로딩 (React.lazy) |
| Suspense          | 로딩 상태를 처리하는 컴포넌트            |
| 동적 import       | 조건부/동적 로딩 가능 (`import()`)       |
| React Router 연계 | 페이지별 코드 분할을 라우팅과 함께 처리  |

> React의 Lazy Loading과 Code Splitting은 성능 개선과 사용자 경험 향상에 핵심적인 전략입니다. 실제 서비스에 적극 활용해보세요! ✨
