### 프로그래밍 언어 차원에서 본다면 데이터들을 잘 관리할 수 있도록 순서를 정해서 관리하는 데이터 타입의 하나

</br>

# 리스트를 만드는 방법

### 대괄호 이용

```
a = [1, 2, 3, 4, 5]
b = ['blockdmask', 2, 4, 'blog']
c = [] #비어있음
```

</br>

# 파이썬 list의 사칙연산

### 1. 덧셈

```
# 리스트 덧셈
a = ["BlockDMask", 333]
b = [1, 2, 3]

print(a + b)

#BlockDMask, 333, 1, 2, 3
```

### 2. 곱셈

```
# 리스트
a = [1, 2, 3]

b = a * 3
print(b)

c = a * 0
print(c)​

#[1, 2, 3, 1, 2, 3, 1,2 3]
#[]
```

</br>

# list 인덱싱, list 슬라이싱

### list 인덱싱 1 - list 검색/ 접근

: 파이썬의 리스트는 시퀀스 데이터 타입이기 때문에 인덱스를 이용해서 접근

```
# 리스트 인덱싱
# 길이가 8인 리스트
a = [101, 102, 'b', 'l', 'o', 103, 104, 105]

# 인자 접근
print(f'a[0] : ')
print(f'a[1] : ')
print(f'a[2] : ')
# ...
print(f'a[7] : ')

# print(f'a[8] : ') - error


# 그럼 마이너스로 접근이 가능할까요?
print(f'a[-1] : ')
print(f'a[-2] : ')
# ...
print(f'a[-8] : ')

# print(f'a[-9] : ') - error
```

### list 인덱싱 2 - list 값 수정

: 인덱싱을 가지고 리스트의 특정 요소의 값을 수정

```
# 리스트 값 수정
b = [222, 333, 444, 555]

print(f'b : \n')

b[0] = 10
print(f'b[0] = 10')
print(f'b : \n')

b[-2] = 'BlockDMask'
print(f'b[-2] = \'BlockDMask\'')
print(f'b : \n')

b[3] = 1000
print(f'b[3] = 1000')
print(f'b : ')

##
# b : [222, 333, 444, 555]

# b[0] = 10
# b : [10, 333, 444, 555]

# b[-2] = 'BlockDMask'
# b : [10, 333, 'BlockDMask', 555]

# b[3] = 1000
# b: [10, 333, 'BlockDMask', 1000]
```

### list 슬라이싱

: 리스트 슬라이싱이라는것은 리스트를 잘라버린다는것

-> 리스트[원하는 시작 index : 원하는 끝 index + 1] 를 하면 해당 리스트의 원하는 부분을 잘라서 리스트로 반환해주는것

```
# 리스트
# 길이가 8인 리스트
a = [101, 102, 'b', 'l', 'o', 103, 104, 105]

# a[1] 부터 ~ a[2] 까지 슬라이싱
print(f'a[1:3] : ')

# a[1] 부터 ~ a[6] 까지 슬라이싱
print(f'a[1:7] : ')

# a[1] 부터 ~ a[7] 까지 슬라이싱 (리스트 끝 까지1)
print(f'a[1:8] : ')

# a[1] 부터 리스트 끝까지 슬라이싱 (리스트 끝 까지2)
print(f'a[1:] : ')

# 리스트 맨 앞에서 부터 맨 뒤 끝 까지
print(f'a[:] : ')

# 리스트 맨 앞에서 특정 부분 까지
print(f'a[:3] : \n')

# 리스트 반으로 뚝딱 나누기 1
print(f'a[:4] : ') # al:4] : [101, 102, 'b', 1']
print(f'a[4:] : ') # a[4:] : ['0', 103, 104, 105]

# 리스트 반으로 나누기 2
# 리스트 길이를 가지고 오는 len 내장함수 이용
w = int(len(a) / 2)
print(f'a[:w] : ') # al:w] : [101, 102, b', 1']
print(f'a[w:] : \n') # a[w:] : ['o', 103, 104, 105]

# 마이너스는 통할까?
print(f'a[-2:] : ') # a[-2:] : [104, 105]
print(f'a[-1:] : ') # a[-1:] : [105]
print(f'a[-5:-1] : ') # a[-5:1] : ['l', 'o', 103, 104]
print(f'a[-5] : ') ['l', 'o', 103, 104] # a[-5] : ['l', 'o', 103, 104]
```

</br>

# 파이썬 리스트의 길이, 삭제

### len 함수 - 리스트의 길이를 구하는 함수

```
# 리스트 길이 구하기
c = [1, 2, 3, 4, 5, 6, 7]

print(f"c : ") # c : [1, 2, 3, 4, 5, 6, 7]
print(f"len(c) : ") # len(c) : 7
```

### del 함수 - 리스트의 특정 요소 혹은 리스트 특정 범위를 삭제

```
# 리스트 삭제, 특정 위치 삭제, 특정 범위 삭제
c = [100, 200, 300, 400, 500, 600, 700]
print(f"c : ") #c : [100, 200, 300, 400, 500, 600, 7001

# 특정 위치 삭제
del(c[1])
print(f"del(c[1])") # del(c[1]) #del(c[1])
print(f"c : \n") # c: [100, 300, 400, 500, 600, 700]

# 범위 삭제
del(c[1:4])
print(f"del(c[1:4])") # del(c[1:4])
print(f"c : \n") # с : [100, 600, 700]
```

</br>

# 리스트 메서드: append, insert, remove, pop, extend

### list.append(x) - 리스트에 값 추가

```
a = [2, 9, 4]
print(a) # [2, 9, 4]

a.append('k')
print(a) # [2, 9, 4, 'k']

a.append(100)
print(a) # [2, 9, 4, 'k', 100]
```

### list.insert(a, b) - 특정 위치에 값 추가

```
c = [22, 44, 66, 88]
print(c) # [22, 44, 66, 88]

c.insert(0, 'k')
print(c) # ['k', 22, 44, 66, 88]

c.insert(3, 'm')
print(c) # ['k', 22, 44, 'm', 66, 88]
```

### list.remove(x) - 리스트에서 특정 값 제거

```
c = [22, 44, 66, 88, 44, 11, 44]
print(f'c            : ') # c            : [22, 44, 66, 88, 44, 11, 44]

# remove() 값이 하나일때
c.remove(66)
print(f'c.remove(66) : ') # c.remove(66) : [22, 44, 88, 44, 11, 44]

# remove() 값이 두개 이상일때
c.remove(44)
print(f'c.remove(44) : ') # c.remove(44) : [22, 88, 44, 11, 44]

# remove() 값이 없을때 (error)
c.remove(1000)
print(f'c.remove(1000) : ') #error
```

### list.pop() - 리스트 맨 마지막 값 반환 후 삭제

```
a = [9, 8, 7, 6, 5]
print(f'a : \n') # a : [9, 8, 7, 6, 5]

b = a.pop()
print(f'a.pop()의 반환 : ') # a.pop()의 반환 : 5
print(f'a : \n') # a : [9, 8, 7, 6]

c = a.pop()
print(f'a.pop()의 반환 : ') # a.pop()의 반환 : 6
print(f'a : \n') # a : [9, 8, 7]


d = a.pop()
print(f'a.pop()의 반환 : ') # a.pop()의 반환 : 7
print(f'a : \n') # a : 19, 8]
```

### list.extend(list2) - 리스트에 다른 리스트2 연결

```
a = [6, 5]
b = [3, 2, 1]
c = ['blockdmask', 'blog']

print(a) # [6, 5]

a.extend(b)
print(a) # [6, 5, 3, 2, 1]

a.extend(c)
print(a) # [6, 5, 3, 2, 1, 'blockdmask', 'blog']
```

# 파이썬 메서드: copy, reverse, sort, count, index, clear

### list.copy() - 리스트 복사

```
a = [100, 200, 300]
b = a.copy()

print(a)
print(b)
print(id(a)) #주소값
print(id(b))

##
#[100, 200, 300]
#[100, 200, 300]
#46587560
#47527752
```

### list.reverse() - 리스트 뒤집기

```
a = [100, 200, 300]
a.reverse()

print(a) # [300, 200, 100]
```

### list.sort() - 리스트 정렬

기본적으로는 오름차순으로 정렬

```
# 정렬 가능!
a = [300, 200, 800, 400, 500, 100]
a.sort()

print(a) # [100, 200, 300, 400, 500, 800]

# 정렬 가능!
b = ['c', 'fff', 't', 'k', 'a']
b.sort()

print(b) # ['a', 'c', 'fff', 'k', 't']

# 정렬 불가능!
c = ['a', 100, 1, 5, 'c', 'b', 'l', 'o']
c.sort()

print(c) #error
```

### list.count(x) - 리스트 값 x 의 개수 세기

```
a = ['b', 'l', 'o', 'c', 'k', 'd', 'm', 'a', 's', 'k']
print(f"a = ") # ['b', 'l', 'o', 'c', 'k', 'd', 'm', 'a', 's', 'k']

# 리스트에서 'k' 개수 찾기
print(f"a.count('k') : ") # a.count('k') : 2

# 리스트에는 없는 'z' 개수 찾기
print(f"a.count('z') : ") # a.count('z') : 0
```

### list.index(x) - 리스트 값 x의 위치(index) 값 반환

```
a = ['b', 'l', 'o', 'c', 'k', 'd', 'm', 'a', 's', 'k']
print(f"a = ") # a = ['b', 'L', 'O', 'C', 'k', 'd', 'n', 'a', 's', 'k']

# 리스트에서 'k' 위치 찾기 (하나인 경우)
print(f"a.index('d') : ") # a. index('d') : 5

# 리스트에서 'k' 위치 찾기 (여러개인 경우)
print(f"a.index('k') : ") # a. index('k') : 4

# 리스트에서 'z' 위치 찾기 (없는 경우)
print(f"a.index('z') : ") #error
```

### list.clear() - 리스트에 저장된 모든 값 삭제

```
a = ['blockdmask', 1, 2, 3]
print(a) # ['blockdmask', 1, 2, 3]

a.clear()
print(a) # []
```

</br>

# 최대, 최소

```
import sys
n = int(sys.stdin.readline())
n_list = list(map(int,sys.stdin.readline().split()))

print(min(n_list), max(n_list))

# 여러개중에 max를 찾는 방법
 result = max(result,sum(x)) #result와 sum 중에서 더 큰 수가 result가 됨
```

</br>

# 교환 swap

### 파이썬 list의 각 요소 교환

```
array = [1, 2 ]
# array의 0번 요소와 1번 요소 교환
array[0], array[1] = array[1], array[0]
```

## 파이썬 리스트 깊은 복사과 얕은 복사

**깊은 복사**는 말 그대로 복사를 해서 각각 독립적인 리스트가 되는것
</br>
**얕은 복사**는 복사는 했지만 얕게 해서 겉에만 복사된 느낌이고 실제로는 같은 리스트를 가리키고 있는것

```
리스트 a가 있었고 a를 복사한 리스트 b가 있다고 했을때
b의 값을 변경했을때 a가 바뀐다 -> 얕은복사 a가 안바뀐다 -> 깊은복사
```

```
좀더 깊게 이야기하면
얕은 복사를 하면 복사가 아닌 참조가 되어서, 같은 주소를 가리키는 변수가 하나 생긴것 뿐입니다.
깊은 복사는 새롭게 리스트를 복사하여 주소값이 아예 다른 별개의 변수가 생긴 것입니다.
```
