# 클로저(Closure)

## 1. 클로저란?

**클로저(Closure)**는 **함수가 선언될 때의 렉시컬 환경(Lexical Environment)을 기억하고, 그 환경에 접근할 수 있는 함수**입니다.

쉽게 말해, **외부 함수의 변수에 접근할 수 있는 내부 함수**를 의미합니다.

## 2. 클로저 예제

```javascript
function outer() {
  let count = 0;

  return function inner() {
    count++;
    console.log(count);
  };
}

const counter = outer();
counter(); // 1
counter(); // 2
counter(); // 3
```

- `inner` 함수는 `outer` 함수의 변수 `count`에 접근할 수 있으며,
- `outer()`가 실행된 후에도 `count` 변수는 사라지지 않고 유지됩니다.

## 3. 왜 클로저를 사용할까?

### ✅ 데이터 은닉 및 캡슐화

```javascript
function createCounter() {
  let count = 0;

  return {
    increment: function () {
      count++;
      return count;
    },
    decrement: function () {
      count--;
      return count;
    },
  };
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.decrement()); // 0
```

- 외부에서는 `count` 변수에 직접 접근할 수 없습니다.
- `increment`, `decrement` 함수를 통해서만 접근 가능 → **정보 은닉**

### ✅ 상태 유지

```javascript
function makeGreeting(name) {
  return function () {
    console.log(`안녕하세요, ${name}님!`);
  };
}

const greetHyeroung = makeGreeting("혜령");
greetHyeroung(); // 안녕하세요, 혜령님!
```

- `name`은 `makeGreeting`의 실행 컨텍스트에서 선언되었지만,
- `greetHyeroung`이 실행될 때 여전히 접근 가능 → **상태를 유지**

## 4. 주의할 점: 메모리 누수

클로저는 참조를 유지하므로 **불필요한 참조**가 많아지면 **메모리 누수**가 발생할 수 있습니다.

```javascript
function badClosure() {
  const largeData = new Array(1000000).fill("💥");
  return () => {
    console.log(largeData[0]);
  };
}

const leaky = badClosure();
// largeData는 계속 메모리에 남아 있음
```

➡ 필요하지 않다면 클로저 사용을 피하거나, 참조를 명확히 제거해야 합니다.

## 5. 클로저와 루프 변수 문제

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
} // 모두 3 출력
```

`var`는 함수 스코프이기 때문에 클로저는 `i`의 최종 값 `3`을 참조하게 됩니다.

### 해결 방법: `let` 또는 IIFE 사용

```javascript
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
} // 0, 1, 2 출력
```

## 6. 결론

- 클로저는 **외부 함수의 변수를 기억하는 함수**
- **데이터 은닉**, **상태 유지** 등에 유용하게 사용
- 클로저를 사용하면 강력하지만, **메모리 누수**나 **의도하지 않은 참조**를 주의

➡ 클로저를 이해하면 JavaScript의 **스코프, 실행 컨텍스트, 메모리 관리**까지 깊이 있게 다룰 수 있음
