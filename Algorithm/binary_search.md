# 탐색 알고리즘: 이진 탐색 (Binary Search)

## 🔍 개요

이진 탐색은 **정렬된 배열**에서 특정 값을 빠르게 찾는 효율적인 알고리즘입니다. 일반적인 순차 탐색(Linear Search)은 O(n)의 시간 복잡도를 가지는 반면, 이진 탐색은 O(log n)으로 매우 빠릅니다.

---

## 📌 전제 조건

- 배열이 **오름차순 또는 내림차순으로 정렬되어 있어야** 이진 탐색이 가능합니다.

```js
// 오름차순 정렬된 배열 예시
const arr = [1, 3, 5, 7, 9, 11, 13];
```

---

## ⚙️ 동작 원리

1. 배열의 **중간값(middle)** 을 선택합니다.
2. 찾고자 하는 값이 중간값보다 작으면 **왼쪽 절반**을,
3. 크면 **오른쪽 절반**을 기준으로 탐색을 반복합니다.
4. 찾는 값이 중간값과 같으면 해당 인덱스를 반환합니다.
5. 범위가 더 이상 없으면 -1 또는 실패 신호를 반환합니다.

---

## 📘 구현 (JavaScript)

```js
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    const mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) {
      return mid; // 값을 찾았을 경우 인덱스 반환
    } else if (arr[mid] < target) {
      left = mid + 1; // 오른쪽 절반 탐색
    } else {
      right = mid - 1; // 왼쪽 절반 탐색
    }
  }

  return -1; // 값을 찾지 못한 경우
}

const arr = [1, 3, 5, 7, 9, 11, 13];
console.log(binarySearch(arr, 7)); // 출력: 3
```

---

## ⏱ 시간 복잡도 분석

| 케이스         | 시간 복잡도                  |
| -------------- | ---------------------------- |
| 최선 (Best)    | O(1) — 첫 비교에서 찾는 경우 |
| 평균 (Average) | O(log n)                     |
| 최악 (Worst)   | O(log n)                     |

> 매 반복마다 탐색 범위가 절반으로 줄어들기 때문에 log₂(n) 횟수의 비교만으로도 결과를 얻을 수 있음

---

## 📦 응용 사례

- 사전 검색 기능 (예: 자동완성 추천)
- 데이터베이스의 인덱싱 시스템
- 문제 풀이에서 범위 내 최적값 찾기 (파라메트릭 서치)
- 정렬된 로그 파일에서 특정 로그 검색

---

## 🧠 재귀로 구현하기

```js
function binarySearchRecursive(arr, target, left = 0, right = arr.length - 1) {
  if (left > right) return -1;

  const mid = Math.floor((left + right) / 2);

  if (arr[mid] === target) return mid;
  else if (arr[mid] < target)
    return binarySearchRecursive(arr, target, mid + 1, right);
  else return binarySearchRecursive(arr, target, left, mid - 1);
}

console.log(binarySearchRecursive([1, 3, 5, 7, 9], 9)); // 출력: 4
```

---

## ⚠️ 주의 사항

- 배열이 **정렬되어 있지 않다면**, 이진 탐색은 제대로 동작하지 않습니다.
- 배열이 너무 크거나 무한이라면 탐색 범위를 잘 제어해야 합니다.
- 오버플로 방지를 위해 중간값 계산 시 `mid = left + Math.floor((right - left) / 2)` 형태로 쓰는 것을 권장하기도 합니다.

---

## ✅ 정리

| 항목        | 내용                           |
| ----------- | ------------------------------ |
| 입력 조건   | 정렬된 배열                    |
| 시간 복잡도 | O(log n)                       |
| 주요 특징   | 탐색 범위를 매번 절반으로 줄임 |
| 구현 방식   | 반복문 또는 재귀함수 사용 가능 |

> 이진 탐색은 단순하면서도 매우 강력한 알고리즘으로, 다양한 문제 해결의 기반이 됩니다. 꼭 숙지해야 할 기본 탐색 알고리즘입니다. 🔍
