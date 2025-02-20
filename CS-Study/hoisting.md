## ⭐ 1. 호이스팅(Hoisting)과 발생하는 이유

### 🔹 호이스팅이란?

호이스팅(Hoisting)이란 **JavaScript 엔진이 코드를 실행하기 전에 변수와 함수 선언을 메모리의 최상단으로 끌어올리는 현상**을 의미합니다.

### 🔹 발생하는 이유

- JavaScript의 **인터프리터(Interpreter)**가 실행 전에 코드 스캔을 하면서 변수 및 함수 선언을 메모리에 등록하기 때문입니다.
- 실제 코드 작성 순서와 다르게 실행될 수 있습니다.

### ✅ 예제

```javascript
console.log(a); // undefined
var a = 10;
console.log(a); // 10
```

</br>

## 2. 스코프(Scope)

### 🔹 스코프란?

**스코프(Scope)**란 변수에 접근할 수 있는 유효 범위를 의미합니다.

### 🔹 스코프의 종류

    1.	전역 스코프(Global Scope): 코드 어디서든 접근 가능
    2.	지역 스코프(Local Scope): 특정 블록 내부에서만 접근 가능

### ✅ 예제

```javascript
var globalVar = "나는 전역 변수";

function localScope() {
  let localVar = "나는 지역 변수";
  console.log(localVar); // 가능
}

console.log(globalVar); // 가능
console.log(localVar); // 오류 발생 (localVar is not defined)
```

### 1) 전역 스코프(Global Scope)

    •	코드 어디에서든 접근 가능한 변수의 범위**를 의미합니다.
    •	전역 스코프에 선언된 변수는 프로그램이 종료될 때까지 메모리에 남아 있습니다.

### ✅ 예제

```javascript
var globalVar = "나는 전역 변수";

function example() {
  console.log(globalVar); // 나는 전역 변수
}

example();
console.log(globalVar); // 나는 전역 변수
```

### 2) 지역 스코프(Local Scope)

    •	특정 블록 내부에서만 접근할 수 있는 변수의 범위를 의미합니다.
    •	함수 내부에서 선언된 변수는 함수 바깥에서 접근할 수 없습니다.

✅ 예제

```javascript
function localScope() {
  let localVar = "나는 지역 변수";
  console.log(localVar); // 나는 지역 변수
}

localScope();
console.log(localVar); // 오류 발생 (localVar is not defined)
```

### 3) 블록 스코프(Block Scope)

    •	{} 블록 내부에서 선언된 변수는 해당 블록 내에서만 접근 가능합니다.
    •	let, const 키워드로 선언된 변수는 블록 스코프를 가집니다.

✅ 예제

```javascript
if (true) {
  let blockVar = "나는 블록 변수";
  console.log(blockVar); // 나는 블록 변수
}

console.log(blockVar); // 오류 발생 (blockVar is not defined)
```

</br>

## ⭐ 3. 함수 스코프(Function Scope) vs 블록 스코프(Block Scope)

    •	var 키워드는 함수 스코프를 가집니다. (함수 내부에서만 유효)
    •	let, const 키워드는 블록 스코프를 가집니다. (블록 {} 내부에서만 유효)

✅ 예제

```javascript
function functionScope() {
  var functionVar = "나는 함수 변수";
  console.log(functionVar); // 나는 함수 변수
}

functionScope();
console.log(functionVar); // 오류 발생 (functionVar is not defined)
```
