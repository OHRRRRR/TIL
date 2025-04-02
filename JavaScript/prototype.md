# 프로토타입(Prototype)

## 1. 프로토타입이란?

JavaScript에서 모든 객체는 다른 객체를 상속받을 수 있으며, 이 상속을 제공하는 메커니즘이 **프로토타입(Prototype)** 입니다. JavaScript는 클래스 기반이 아닌 **프로토타입 기반 언어**입니다.

## 2. 프로토타입 체인(Prototype Chain)

객체에서 프로퍼티나 메서드를 찾을 때, **해당 객체 자체에서 먼저 검색**하고, 없으면 프로토타입 체인을 따라 부모 객체에서 검색합니다.

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function () {
  console.log(`Hello, my name is ${this.name}`);
};

const user = new Person("혜령");
user.sayHello(); // Hello, my name is 혜령
```

- `user` 객체에는 `sayHello` 메서드가 없지만, **Person의 프로토타입**에 정의되어 있어 접근이 가능합니다.

## 3. 프로토타입 상속

객체의 프로토타입을 직접 설정하여 상속할 수도 있습니다.

```javascript
const animal = {
  makeSound() {
    console.log("동물이 소리를 냅니다.");
  },
};

const dog = Object.create(animal);
dog.bark = function () {
  console.log("멍멍!");
};

dog.makeSound(); // 동물이 소리를 냅니다.
dog.bark(); // 멍멍!
```

- `dog` 객체는 `animal`을 프로토타입으로 가지므로, `makeSound()`를 사용할 수 있습니다.

## 4. `__proto__`와 `Object.getPrototypeOf()`

객체의 프로토타입을 확인하거나 변경하는 방법은 다음과 같습니다.

```javascript
const obj = {};
console.log(obj.__proto__); // 기본적으로 Object.prototype을 가리킴
console.log(Object.getPrototypeOf(obj)); // 같은 결과
```

프로토타입을 수동으로 변경할 수도 있습니다.

```javascript
const cat = {
  sound: "야옹",
};
const kitty = Object.create(cat);
console.log(kitty.sound); // 야옹
```

## 5. 클래스와 프로토타입

JavaScript의 클래스는 내부적으로 프로토타입을 사용하여 동작합니다.

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }
  speak() {
    console.log(`${this.name}이(가) 소리를 냅니다.`);
  }
}

const doggo = new Animal("바둑이");
doggo.speak(); // 바둑이이(가) 소리를 냅니다.
```

클래스를 사용하면 `prototype`을 직접 설정하지 않아도 **자동으로 프로토타입 체인이 구성**됩니다.

## 6. 결론

- JavaScript의 객체는 프로토타입을 기반으로 상속
- `Object.create()`를 사용하면 간편하게 프로토타입을 설정 가능
- `class` 문법은 내부적으로 프로토타입을 활용하여 동작
- **프로토타입을 이해하면 JavaScript의 객체 지향적인 특징을 효과적으로 활용 가능**
