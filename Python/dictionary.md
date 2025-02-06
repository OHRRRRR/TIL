# Dictionary

- 키와 값의 쌍으로 구성된 자료구조

- 키는 유일해야 하며, 값은 중복이 허용됨

- 요소에 접근할 때는 키를 사용

- 중괄호{}를 사용하여 표현

- 키와 값은 콜론:으로 구분

- 순서 없음

- 변경 가능

```
person = {'name':'jhon','age':30, "city":'seoul'}
```

### dict() 함수 사용 방법

```
person = dict('name':'jhon', 'age':30, 'city': 'seoul')

print(person)
//{'name':'jhon', 'age':30, 'city': 'seoul'}
```

### 같은 위치에 있는 요소끼리 묶어서 튜플의 리스트 생성 -> Zip(), Dict() 함수 사용

```
keys = ['name', 'age', 'city']
values = ['jhon', 30, 'seoul']
peson = dict(zip(keys,values))

print(person)
//{'name':'jhon', 'age':30, 'city':'seoul'}
```

### 딕셔너리에 요소 추가

```
person = dict('name':'jhon', 'age':30, 'city': 'seoul')
person['gender'] ='Male'

print(person}
//{'name':'jhon', 'age':30, 'city': 'seoul', 'gender': 'Male'}
```

### 딕셔너리에 요소 변경

```
person = dict('name':'jhon', 'age':30, 'city': 'seoul')
person['age'] ='31

print(person}
//{'name':'jhon', 'age':31, 'city': 'seoul'}
```

</br>

## 딕셔너리 요소 접근

### 1. key를 이용

```
person = dict('name':'jhon', 'age':30, 'city': 'seoul')

print(person['name'])
//'jhon'
```

### 2. get() 메서드 이용

```
person = dict('name':'jhon', 'age':30, 'city': 'seoul')

print(person.get('name'))
//'jhon'

print(person.get('gender'))
//None
```

</br>

## 딕셔너리 요소 제거

### 1. pop() 메서드 이용 -> pop()메서드는 제거된 요소의 값 반환

```
person={'name':'jhon','age':30, 'city':'Seoul'}
person.pop('age')
print(person)
// {'name':'john', 'city':'Seoul'}
```

### 2. del() 메서드 이용 -> del 딕셔너리 이름[key]를 통해 제거

```
person={'name':'jhon','age':30, 'city':'Seoul'}
del.person['age']
print(person)
// {'name':'john', 'city':'Seoul'}
```

### 3. clear() 메서드 이용 -> 모든 요소 제거

```
person={'name':'jhon','age':30, 'city':'Seoul'}
person.clear()
print(person)
// {}
```

</br>

## 딕셔너리 메서드

### 1. 딕셔너리 키를 가져오는 메서드 -> keys() 메서드 사용

```
person={'name':'jhon','age':30, 'city':'Seoul'}

print(person.keys())
//dict_keys(['name','age','city'])
```

### 2. 딕셔너리 값을 가져오는 메서드 -> values() 메서드 사용

```
person={'name':'jhon','age':30, 'city':'Seoul'}

print(person.values())
//dict_values(['jhon',30,'Seoul'])
```

### 3. key와 value를 동시에 처리하는 방법

```
person={'name':'jhon','age':30, 'city':'Seoul'}

for key.value in person.items():
	print("{key}:{value}")

// name:jhon
// age:30
// city:Seoul
```

</br>

## 딕셔너리 응용 사용

### 1. 중첩 딕셔너리

```
person={'name':'jhon','age':30, 'address':{'city':'Seoul', 'street':'123 Main st'}}
```

### 2. 딕셔너리 특정 키 존재 확인

````
person={'name':'jhon','age':30, 'city':'Seoul'}

if 'age' in person:
	print("age in person")
else:
	print("not in person")
    ```
````
