## ⭐ 1. 데이터 형변환(Type Conversion)

### 데이터 형변환이란?

JavaScript에서 **데이터 형변환(Type Conversion)**이란 **값의 데이터 타입을 다른 타입으로 변환하는 과정**을 의미합니다.  
자바스크립트에서는 **명시적 형변환(Explicit Conversion)**과 **암묵적 형변환(Implicit Conversion)**이 발생할 수 있습니다.

---

### 1) 명시적 형변환 (Explicit Conversion)

- 개발자가 **명확하게 타입 변환을 수행하는 것**을 의미합니다.
- `String()`, `Number()`, `Boolean()` 등의 메서드를 사용하여 변환합니다.

### ✅ 예제

```javascript
// 숫자를 문자열로 변환
let num = 10;
console.log(String(num)); // "10"

// 문자열을 숫자로 변환
let str = "20";
console.log(Number(str)); // 20

// 다른 값들을 Boolean으로 변환
console.log(Boolean(1)); // true
console.log(Boolean(0)); // false
console.log(Boolean("")); // false
console.log(Boolean("Hello")); // true
```

### 2) 암묵적 형변환 (Implicit Conversion)

- JavaScript가 자동으로 타입을 변환하는 것을 의미합니다.
- 보통 연산자 사용 시 발생합니다.

### ✅ 예제

```
// 숫자와 문자열을 더하면 문자열이 됨
console.log(5 + "5"); // "55"

// 문자열을 숫자로 변환 후 연산 수행
console.log("10" - 5); // 5
console.log("10" * 2); // 20

// Boolean 변환
console.log(!!"Hello"); // true
console.log(!!0); // false
```

</br>

## ⭐ 2. 자바스크립트가 동적 언어인 이유

### 동적 언어(Dynamic Language)란?

JavaScript는 **동적 타입 언어(Dynamically Typed Language)** 입니다.
즉, 변수를 선언할 때 데이터 타입을 명시할 필요가 없고, 실행 중에 타입이 변경될 수 있습니다.

### ✅ 예제

```
let variable = 10;  // 숫자 타입
console.log(typeof variable); // "number"

variable = "Hello"; // 문자열로 변경
console.log(typeof variable); // "string"

variable = true; // 불리언으로 변경
console.log(typeof variable); // "boolean"
```

</br>

## ⭐ 3. 프로토타입(Prototype)

### 1) 프로토타입이란?

JavaScript에서 객체는 프로토타입이라는 속성을 이용해 다른 객체로부터 속성과 메서드를 상속받을 수 있습니다.
이는 **프로토타입 기반 객체지향 프로그래밍(Prototype-based OOP)** 을 가능하게 합니다.

### 2) 프로토타입 체인(Prototype Chain

- 자바스크립트 객체는 다른 객체를 자신의 **프로토타입(proto)** 으로 설정하여 상속을 구현합니다.
- 객체에서 특정 프로퍼티를 찾을 때, 현재 객체에 없으면 프로토타입 체인을 따라 상위 객체에서 검색합니다.
- ### ✅ 예제

```
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  return `Hello, my name is ${this.name}`;
};

const user = new Person("Alice");

console.log(user.greet()); // "Hello, my name is Alice"
console.log(user.__proto__ === Person.prototype); // true
```

-> 객체가 생성될 때 prototype을 상속받으며, 프로토타입 체인을 통해 메서드를 호출할 수 있습니다.
