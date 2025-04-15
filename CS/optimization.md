# 🧠 Optimization in Computer Science

## 📌 개요

최적화(Optimization)는 제한된 자원(시간, 메모리, 에너지 등) 내에서 성능을 극대화하거나 비용을 최소화하기 위한 기법입니다. 컴퓨터 과학 전반에서 매우 중요한 개념으로, 소프트웨어와 하드웨어, 알고리즘, 네트워크, 운영체제 등 다양한 분야에 적용됩니다. 이 문서에서는 **CS에서의 최적화 개념**과 함께 **각 영역별 최적화 기법**들을 구체적으로 정리합니다.

---

## 🧱 1. 알고리즘 최적화

### 🔍 개념

- 더 적은 시간과 공간을 사용하는 알고리즘으로 교체하거나 개선하는 과정

### 💡 대표 기법

- 시간 복잡도 개선: O(n²) → O(n log n)
- 메모이제이션, 다이나믹 프로그래밍 (DP)
- 분할 정복, 탐욕 알고리즘
- 데이터 구조 개선: 배열 → 해시 테이블 / 트리

### 📘 예시

- 피보나치 수열 계산: 재귀 → DP로 개선 (시간 복잡도 O(2ⁿ) → O(n))
- 정렬 알고리즘: 버블 정렬 → 퀵 정렬

---

## 🧮 2. 코드 최적화 (Code Optimization)

### 🔍 개념

- 동일한 기능을 더 빠르고 효율적으로 수행하도록 코드 수정

### 💡 대표 기법

- 불필요한 연산 제거
- 루프 언롤링(Loop Unrolling)
- Dead Code 제거
- 상수 폴딩(Constant Folding)
- Inline 함수 사용

### ⚠️ 주의할 점

- 가독성 저하를 일으킬 수 있어 유지보수성도 고려해야 함

### 📘 예시

```javascript
// Before
for (let i = 0; i < arr.length; i++) {
  if (arr[i] === 5) console.log("found");
}

// After
const found = arr.includes(5);
if (found) console.log("found");
```

---

## 💽 3. 메모리 최적화

### 🔍 개념

- 사용되는 메모리 용량을 줄이거나 메모리 접근 속도를 개선

### 💡 대표 기법

- 구조체 패딩 제거
- 데이터 압축
- 참조 타입 최소화
- 객체 풀링(Object Pooling)

### 📘 예시

- 불필요한 배열/객체 생성 방지
- 문자열을 `StringBuilder`처럼 누적하여 처리
- 자바스크립트에서 `Map`/`Set`으로 중복 제거

---

## ⚙️ 4. 컴파일러 최적화

### 🔍 개념

컴파일 시점에 프로그램의 성능을 자동으로 향상시키는 기법들

### 💡 대표 기법

- 루프 최적화 (Unrolling, Fusion, Invariant 이동)
- 상수 전파(Constant Propagation)
- 공통 부분식 제거(Common Subexpression Elimination)

### 📘 예시

- `gcc -O2`, `clang -O3` 등의 컴파일 옵션
- JIT(Just-In-Time) 컴파일러의 실행 중 최적화

---

## 🖥️ 5. 시스템/운영체제 레벨 최적화

### 🔍 개념

하드웨어와 OS 간의 상호작용 최적화

### 💡 대표 기법

- 캐시 활용: L1/L2/L3 캐시, CPU Cache Locality
- 메모리 정렬 및 페이지 교체 알고리즘 개선
- 스레드/프로세스 간 병렬 처리
- I/O 스케줄링

### 📘 예시

- SSD의 입출력 큐 관리 최적화
- context switching 최소화
- 메모리 접근 시간 최적화를 위한 구조체 정렬

---

## 🌐 6. 네트워크 최적화

### 🔍 개념

데이터 전송 속도 및 네트워크 효율성을 향상

### 💡 대표 기법

- 압축, CDN, 캐시 전략
- DNS 최적화
- Lazy loading, prefetching

### 📘 예시

- 이미지 lazy load로 초기 렌더링 시간 감소
- HTTP/2를 이용한 병렬 전송

---

## 📱 7. 프론트엔드 성능 최적화

### 🔍 개념

사용자 경험을 고려한 클라이언트 측 최적화

### 💡 대표 기법

- 코드 스플리팅(code splitting)
- tree shaking
- Debounce, Throttle
- Re-render 방지 (React에서 memo, useCallback 등)
- 웹폰트 최적화

### 📘 예시

- Next.js의 SSR/SSG로 초기 로딩 속도 향상
- React의 Virtual DOM diffing 최적화

---

## 🛠️ 성능 측정 도구 및 기법

### ✅ 코드/시스템 단위

- Lighthouse (웹 성능)
- Chrome DevTools
- 프로파일러 (CPU, Heap, Network)
- Benchmark.js (JS 성능 측정)
- Sentry, Hotjar (사용자 흐름 분석)

### ✅ 정량 지표

- 처리 시간 (Latency)
- 처리량 (Throughput)
- CPU 사용량
- 메모리 사용량

---

## 🧭 결론

컴퓨터 과학에서 최적화는 "효율"과 직결됩니다. 사용자 경험, 자원 활용, 확장성, 유지보수성 등 전반에 걸친 성능 향상을 위해 다양한 최적화 기법들이 필요합니다. 단순한 개선이 아닌, 전체 시스템 아키텍처와 코드의 흐름을 이해한 상태에서 적용하는 것이 핵심입니다.

---

## 📚 참고자료

- [Optimizing Software in C++ by Agner Fog](https://www.agner.org/optimize/optimizing_cpp.pdf)
- [Google Web Fundamentals – Performance](https://developers.google.com/web/fundamentals/performance)
- [Clean Code by Robert C. Martin](https://www.oreilly.com/library/view/clean-code/9780136083238/)
- [MDN Web Docs - Performance](https://developer.mozilla.org/en-US/docs/Web/Performance)

---

## ❓ 심화 질문

**Q1:** 알고리즘 최적화와 코드 최적화는 어떤 상황에서 서로 충돌할 수 있을까요?

**Q2:** 자바스크립트 프론트엔드 개발 시 React 렌더링 최적화를 어떻게 측정하고 판단하나요?

**Q3:** 시스템 자원이 무제한일 때도 최적화가 필요한 이유는 무엇인가요?
