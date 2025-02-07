## 특징

1. 순서가 없음 -> 인덱스로 접근할 수 없다.

2. 중복은 허용되지 않음

3. 요소는 변경 불가능한 자료형만 사용할 수 있음

## 사용

1. set() 함수 사용

```
   set_example = set([1,2,3,4,5])
   print(set_example)

>> {1,2,3,4,5}
```

2. 집합에 직접 값 할당

```
   set_example = {1,2,3,4,5}
   print(set_example)
>> {1,2,3,4,5}
```

## 집합의 요소 접근

-> 순서가 지정되지 않으므로 인덱스로 접근 불가 -> 반복문 사용해서 접근

```
set_example = {1,2,3,4,5}
for i in set_example:
	print(i)

>>
    1
    2
    3
    4
    5
```

## in 연산자를 이용한 요소 확인

```
fruits = {"apple", "banana", "cherry"}
print("apple" in fruits)
print("grape" in fruits)

>>True
>>False
```

## 집합에 요소 추가

### 1. 요소 1개 추가 -> add()메서드 사용

```
set_example = {1,2,3,4,5}
set_example.add(6)
print(set_example)

>> {1,2,3,4,5}
```

### 2. 요소 여러개 추가 -> update()메서드 사용

```
set_example = {1,2,3,4,5}
set_example.update([6,7,8])
print(set_example)

>> {1,2,3,4,5,6,7,8}
```

## 집합에서 요소 제거

### 1. remove() 메서드 사용 -> 요소가 집합에 없으면 keyError 발생

```
set_example = {1,2,3,4,5}
set_example.remove(5)
print(set_example)

>>{1,2,3,4}
```

### 2. discard() 메서드 사용 -> 요소가 세트에 존재하지 않는 경우 keyError를 발생시키지 않음

```
set_example = {1,2,3,4,5}
set_example.discard(6)
print(set_example)

>>{1,2,3,4,5}
```

### 3. pop() 메서드 사용 -> 맨 앞의 요소가 제거됨

```
set_example = {1,2,3,4,5}
set_example.pop()
print(set_example)

>>{2,3,4,5}
```

</br>

## 합집합, 교집합, 차집합

### 1. 합집합

```
set_a = {1,2,3,4,5}
set_b = {4,5,6,7,8}
set_c = set_a | set_b

print(set_c)

>>{1,2,3,4,5,6,7,8}
```

### 2. 교집합

```
set_a = {1,2,3,4,5}
set_a = {4,5,6,7,8}

set_c = set_a & set_b

print(set_c)

>>{4,5}
```

### 3. 차집합

```
set_a = {1,2,3,4,5}
set_a = {4,5,6,7,8}

set_c = set_a - set_b

print(set_c)

>>{1,2,3}
```
