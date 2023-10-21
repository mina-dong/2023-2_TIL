# cp2 Sorting

---
- Basic Sorting Algorithms
- Advanced Sorting Algorithms
---


## Basic Sorting Algorithms
### 선택정렬 (Selection Sort) : 배열 A[1…n]에서 가장 큰 원소를 찾아 배열의 끝자리에 있는 A[n]과 치환

```
selectionSort(A[], n) ▷ 배열 A[1 ... n]을 정렬한다
{ 
for last ← n downto 2 { ----------------- ①
A[1 ... last] 중 가장 큰 수 A[k]를 찾는다; ----------- ②
A[k] ↔ A[last]; ▷ A[k]와 A[last]의 값을 교환 -------- ③
} 
}
```

①의 for 루프는 n-1번 반복
②에서 가장 큰 수를 찾기 위한 비교횟수: n-1, n-2, …, 2, 1
③의 교환은 상수 시간 작업


수행 시간: (n-1)+(n-2)+···+2+1 = Θ(n2)


### 버블정렬 (Bubble Sort : 선택정렬처럼 제일 큰 원소를 끝자리로 옮기는 정렬이나, 왼쪽부터 이웃한 수를 비교하며 순서를 바꿔 나가는 형태임. 

(n-1)+(n-2)+···+2+1 = Θ(n2)

### 삽입정렬 (Insertion Sort) :이미 정렬된 i개의 배열에 원소를 하나 더 더해서 i+1개 짜리 배열을 만드는 과정을 반복함

## Advanced Sorting Algorithms

### 병합정렬 (Merge Sort) : 입력을 반으로 나누고, 전반부와 후반부를 독립적으로 정렬하는 방법, **재귀적** 

mergeSort(A[ ], p, r) 
▷ A[p ... r]을 정렬한다.
{ 
if (p < r) then { 
q ← (𝑝𝑝 + 𝑞𝑞)/2 ; ----------------- ① ▷ p, q의 중간 지점 계산
mergeSort(A, p, q); ---------------- ② ▷ 전반부 정렬
mergeSort(A, q+1, r); -------------- ③ ▷ 후반부 정렬
merge(A, p, q, r); ------------------ ④ ▷ 병합
} 
}

T(n) = 2T(𝑛/
2) + n = Θ(nlogn)


### 퀵정렬 (Quick Sort) :평균적으로 가장 좋은 성능을 가진 정렬 알고리즘, 기준원소를 잡고 기준원소를 기준으로 양쪽으로 재배치 하며 정렬하는 방식