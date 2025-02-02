# for,list comprehension 사용한 입력 받기

### 9개의 수를 for문으로 입력 받기

```
numbers = []
for _ in range(9):
    i = int(input())
    numbers.append(i)

print(max(numbers))
print(numbers.index(max(numbers))+1)
```

### for문을 list comprehension 으로 작성한 코드

```
numbers = [int(input()) for _ in range(9)]

print(max(numbers))
print(numbers.index(max(numbers)) + 1)
```

### 문자열 여러줄 입력받기

```
str_list = [input() for _ in range(n)]

## n이 3일 때
# a
# b
# c
```

### 띄어쓰기 없이 정수 여러 개를 입력받아 2차원 배열로 저장하기

```
t_d_array = [list(map(int, input())) for _ in range(n)]

## n이 3일 때
# 123
# 456
# 789
```

### 열은 띄어쓰기로 행은 엔터로 구분하여 입력받아 2차원 배열로 저장하기

```
t_d_array = [list(map(int, input().split())) for _ in range(n)]

## n이 3일 때
# 1 2 3
# 4 5 6
# 7 8 9
```

<br/> 
 <br/> 
 
# List Comprehension
### 1부터 10까지 정수를 순서대로 가지고 있는 리스트를 생성
  ```
# 기존 방식
numbers = []
for n in range(1, 10+1):
    numbers.append(n)
```
```
# list comprehension 사용
[x for x in range(10)]
```

### 2의 배수를 10개 가지고 있는 리스트

```
# 기존 코드
even_numbers = []
for n in range(1, 10+1):
   if n % 2 == 0:
       even_numbers.append(n)
# [2, 4, 6, 8, 10]
```

```
# list comprehension 사용 1
[ 2*x for x in range(1, 10+1) ]
#[2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
```

```
# list comprehension 사용 2
[x for x in range(1, 10+1) if x % 2 == 0]
# [2, 4, 6, 8, 10]
```

### 설명 못했던 코드

```
n = int(input())
graph = [[False]*(n+1) for _ in range(n+1)] # 앞의 n+1씩 뒤의 n+1개의 줄
print(graph)

#n이 3일때 출력
# [[False, False, False, False], [False, False, False, False], [False, False, False, False], [False, False, False, False]]
```
