# 깊은 복사와 얕은 복사 (Deep Copy vs Shallow Copy)

## 얕은 복사(Shallow Copy)

- **객체의 참조(주소값)만 복사**하는 방식입니다.
- 원본 객체와 복사된 객체가 **같은 메모리 주소를 가리킵니다**.
- 따라서 **복사본을 수정하면 원본도 영향을 받습니다**.

### 얕은 복사 예제

```js
const obj1 = { name: "Alice", age: 25 };
const obj2 = obj1; // 얕은 복사

obj2.age = 30;
console.log(obj1.age); // 30 (원본도 변경됨)
```

### Object.assign()

assign은 ‘할당’이라는 뜻을 가지고 있으며 객체와 객체를 합쳐주는 메서드다.

```js
var obj1 = {
  a: 10,
  b: {
    c: "abc",
  },
};
var obj2 = Object.assign({}, obj1);
obj2.a = 20;
obj2.b.c = "def";

console.log(obj1); // { a: 10, b: { c: "def" } }
console.log(obj2); // { a: 20, b: { c: "def" } }
```

- 첫번째 인자로 {} 빈 객체가 들어갔기 때문에 껍데기가 obj1과 다른 객체가 반환 될 것이다.
- obj1의 내용을 {} 빈 객체 안에 복사해서 집어넣고 반환한다.
- 프로퍼티 a는 기본형 타입의 값이 들어있기 때문에 변경하면 obj2의 a 프로퍼티만 변경된다.
- 프로퍼티 b는 참조형 타입의 값이 들어있기 때문에 변경하면 obj1, obj2의 b가 가진 주소값이 동일하기 때문에 둘 다 변경된다.

### for … in

```js
var copyShallo = function (obj) {
  var result = {};
  for (var prop in obj) {
    result[prop] = obj[prop];
  }
  return result;
};
```

</br>

## 깊은 복사(Deep Copy)

여기서 말하는 ’복사‘란, 원본을 베낌. 종이를 포개고 그 사이사이에 복사지를 받쳐 한 번에 여러 장을 쓴다는 의미를 가지고 있다. 즉 동일한 내용을 그대로 다른 곳에서 사용하는 것을 말한다.

그리고, 깊은 복사란, 기존 값의 모든 참조가 끊어지는 것을 말한다. 특히 복사할 때, 참조형 타입 값(객체)에서 내부에 있는 모든 값이 새로운 값이 되는 것을 말한다.

- 객체의 모든 값을 새롭게 복사하는 방식입니다.
- 원본과 복사본이 완전히 독립적인 메모리 공간을 가집니다.
- 복사본을 수정해도 원본에 영향이 없습니다.

### 깊은 복사 예제

```js
const obj1 = { name: "Alice", age: 25, address: { city: "Seoul" } };
const obj2 = JSON.parse(JSON.stringify(obj1)); // 깊은 복사

obj2.address.city = "Busan";
console.log(obj1.address.city); // "Seoul" (원본 유지)
```

### 참조형 타입의 깊은 복사

```js
var obj1 = {
  a: 10,
  b: "abc",
};
var obj2 = obj1;
console.log(obj1 === obj2); // true

obj2.a = 20;
console.log(obj1); // {a: 20, b: 'abc'}
console.log(obj2); // {a: 20, b: 'abc'}
console.log(obj1 === obj2); // true
```

- obj1과 obj2가 가지고 있는 주소 값이 동일하기 때문에 true가 나왔다.
- obj2의 a프로퍼티의 값을 20으로 재할당했다.
- obj1, obj2의 값의 a 프로퍼티 모두 20으로 변경되었다.
- 여전히 obj1과 obj2가 가지고 있는 주소 값이 동일하다.

결과가 나온 이유는, obj2의 ’프로퍼티‘를 변경시켰기 때문이다. 프로퍼티 a가 바라보고 있는 주소 자체는 변경되었지만 obj1, obj2가 프로퍼티 ‘그룹’을 바라보는 주소자체는 변경되지 않은 것이다. 이렇게 객체 자체의 참조 값을 할당하면, 깊은 복사가 일어나지 않는다.

### 재귀 함수를 이용

```js
var deepCopy = function (obj) {
  var result = {};
  if (typeof obj === "object" && obj !== null) {
    for (var prop in obj) {
      result[obj] = deepCopy(obj[prop]);
    }
  } else {
    result = obj;
  }
  return result;
};
```

deepCopy 함수는 함수 내부에서 자기 자신을 호출하는 재귀 함수다. 중첩된 객체라고 하더라도 프로퍼티 갯수만큼 돌면서 result 객체에 새롭게 할당해준다.

## 불변 값

### 불변 값은, 변하지 않는 값이라는 뜻이다. 위에서 살펴본 기본형 타입은 불변 값이다. 그리고 참조형 타입은 대체적으로 가변값이다.

```js
var a = 10;
a = 20;
console.log(a); // 20
```

처음에는 a에 10 값을 주었다. 그리고 20 값을 다시 할당하고 출력하니 20이 나왔다. 자바스크립트 입장에서 설명해보자.

- 메모리 공간을 확보 후 다른 메모리 공간에 10을 할당했다.
- 그리고 10이 저장된 주소를 a에 넣는다.
- 이후, 20을 재할당할 때, 10이 저장되어 있는 메모리 공간을 그대로 두고, 20을 저장하는 메모리 공간을 추가로 확보 후 저장한다.
- 그리고 그 공간의 주소를 a가 저장한다.

흔히 사람의 입장에서는 10이 저장되어 있는 메모리 공간에 10을 삭제하고 20을 집어 넣는 것을 생각한다. 하지만 자바스크립트는 값을 새로 생성하고 주소를 수정해주었다. 즉, 기본형 타입은 새로 생성 되었고 변경되지 않았다.

하지만 레퍼런스 타입은 다르다.

```js
var obj = {
   a: 10,
   b: 'abc',
}
var obj.a = 20;
```

obj의 프로퍼티의 값을 재할당하면, obj이 가지고 있는 메모리 주소는 변경되지 않고 obj.a가 가지고 있는 주소가 변경된다. 즉, ‘새로운 객체’가 만들어진 것이 아니라 기존 객체 내부의 값만 바뀐 것이다.
