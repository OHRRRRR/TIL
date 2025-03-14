> 필요한 계산 값을 저장해두었다가 재사용하는 알고리즘 설계 기법


## 다이나믹 프로그램을 만족하는 조건
 

### 1. 최적 부분 구조

: 큰 문제를 작은 문제로 나눌 수 있으며, 작은 문제의 답을 모아 큰 문제를 해결

ex) 피보나치 수열은 큰 문제인 f(6)을 구하기 위해 작은 문제 f(5), f(4)를 모아서 해결 가능

 

### 2. 중복 부분 문제

: 부분 문제가 중첩되어 등장함. 동일한 작은 문제를 반복적으로 해결해야 함

ex) 피보나치 수열에서 f(4)를 구하기 위해 f(3), f(2)가 호출되고, f(3)을 구하기 위해 f(2), f(1)이 호출될 때 f(2)가 반복 호출되므로 중복 부분 문제 성립

 
1
## 다이나믹 프로그래밍 방식
 

### 1. 탑다운 (하향식, 메모리제이션, 위 -> 아래)

맨 위의 값에서 재귀로 제일 작은 인덱스를 향하는 것
메모이제이션: 한번 계산한 결과를 메모리 공간에 메모함 -> 같은 문제 호출하면 메모한 결과 그대로 가져옴
재귀함수 사용됨

### 2. 보텀업 (상향식, 작은문제 + 작은문제 => 큰 문제가 되는 형식) 

제일 작은 인덱스의 수 부터 목표하는 값으로 향하는 것
반복문 사용됨
 

그리디 알고리즘 -> 내가 생각한 처음 최적의 방법이 끝까지 반례 없이 적용 되는 경우
동적계획법 -> 가능성을 모두 두고 그안에 최솟값을 찾을 수 있음
 
```
활용 - [백준 1453] 1로 만들기
0.15 초 	128 MB	316083	108302	69035	33.038%
문제
 

정수 X에 사용할 수 있는 연산은 다음과 같이 세 가지 이다.

X가 3으로 나누어 떨어지면, 3으로 나눈다.
X가 2로 나누어 떨어지면, 2로 나눈다.
1을 뺀다.
정수 N이 주어졌을 때, 위와 같은 연산 세 개를 적절히 사용해서 1을 만들려고 한다. 연산을 사용하는 횟수의 최솟값을 출력하시오.

입력
첫째 줄에 1보다 크거나 같고, 106보다 작거나 같은 정수 N이 주어진다.

출력
첫째 줄에 연산을 하는 횟수의 최솟값을 출력한다.

예제 입력 1 복사
2
예제 출력 1 복사
1
예제 입력 2 복사
10
예제 출력 2 복사
3
```

문제 이해
n이 10일 때 → -1을 해서 9가 되는 경우 → ...
                   → 2로 나눠서 5가 되는 경우 → ...

=> 연산 가능한 경우의 수가 계속 생기고, F(2)F(3)F(4)와 같은 함수들이 여러 번 호출되므로 DP 사용 가능
 
```
# # 1로 만들기
n = int(input())

d = [0] * (n+1) # d의 인덱스번호가 n이라고 생각했을 때, 그 숫자가 n이 될때까지의 연산횟수를 그 인덱스 값에 저장

for i in range(2, n+1): # 보텀업 방식 (상향식)
  
  d[i] = d[i-1] + 1 # 현재 수에서 1을 빼는 경우
  # 여기서 if 1빼는 방법/ 2나누기 / 3나누기 동등하게 하지 않고 처음에 1을 빼고 시작하는 
  # 이유는 다음에 계산할 나누기가 1을 뺀 값보다 작거나 큼에 따라 교체되기 때문이다.
  # 즉 셋 다 시도하는 방법 맞음

  # 현재 수에서 1을 빼는게 유리한지 나누는 연산을 하는게 좋은지
  if i % 2 == 0:
    d[i] = min(d[i],d[i//2]+1)
  if i%3 == 0:
    d[i] = min(d[i], d[i//3]+1)

print(d[n])
```