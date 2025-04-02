# 이벤트 루프(Event Loop)

## 1. 이벤트 루프란?

이벤트 루프(Event Loop)는 JavaScript의 **비동기 실행을 관리하는 핵심 메커니즘**입니다. JavaScript는 단일 스레드(Single Thread)로 동작하지만, 이벤트 루프를 통해 비동기 작업을 처리할 수 있습니다.

## 2. 이벤트 루프의 동작 방식

이벤트 루프는 다음과 같은 단계로 동작합니다:

1. **Call Stack (호출 스택)**: 실행할 함수들이 쌓이는 공간입니다.
2. **Web APIs (브라우저 환경 제공 기능)**: `setTimeout`, `setInterval`, `fetch`, `DOM 이벤트` 등이 실행됩니다.
3. **Task Queue (태스크 큐, 콜백 큐)**: 비동기 작업이 완료되면 콜백 함수가 여기에 저장됩니다.
4. **Microtask Queue (마이크로태스크 큐)**: `Promise.then`, `MutationObserver`와 같은 미세 작업이 저장됩니다.
5. **이벤트 루프가 동작하여 Call Stack이 비면, Microtask Queue를 먼저 실행한 후 Task Queue를 실행**합니다.

## 3. 이벤트 루프 흐름 예제

```javascript
console.log("1");

setTimeout(() => {
  console.log("2");
}, 0);

Promise.resolve().then(() => {
  console.log("3");
});

console.log("4");
```

### 실행 순서 분석

1. `console.log("1")` 실행 → 출력: `1`
2. `setTimeout` 등록 (0초 후 실행 예정, Task Queue로 이동)
3. `Promise.then` 등록 (Microtask Queue로 이동)
4. `console.log("4")` 실행 → 출력: `4`
5. Microtask Queue 실행 → `console.log("3")` 출력
6. Task Queue 실행 → `console.log("2")` 출력

### 최종 출력 결과

```
1
4
3
2
```

## 4. 마이크로태스크 우선순위

마이크로태스크(Microtask)는 일반 태스크(Task)보다 먼저 실행됩니다.

```javascript
setTimeout(() => console.log("Task Queue"), 0);
Promise.resolve().then(() => console.log("Microtask Queue"));
console.log("Synchronous Code");
```

### 실행 순서

1. `console.log("Synchronous Code")` → 출력: `Synchronous Code`
2. Microtask Queue 실행 → `console.log("Microtask Queue")`
3. Task Queue 실행 → `console.log("Task Queue")`

### 최종 출력 결과

```
Synchronous Code
Microtask Queue
Task Queue
```

## 5. 결론

- JavaScript는 단일 스레드 기반이지만, 이벤트 루프를 통해 비동기 처리를 효율적으로 관리
- **Microtask Queue**는 **Task Queue**보다 우선 실행
- 이벤트 루프를 이해하면 `setTimeout`, `Promise`, `async/await` 등의 동작을 예측 가능
