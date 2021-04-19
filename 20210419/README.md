# 2021.04.19.

- **문제 사이트** : 

  - [x] SWEA

    - [x] 5204 병합 정렬
    - [ ] 5205 퀵 정렬
    - [ ] 5207 이진 탐색
    - [x] 부분집합 만들기
    - [x] 1486 장훈이의 높은 선반
    - [ ] 15686 치킨 배달
    

- **사용한 알고리즘**

  - 분할 정복 / 백트래킹 




## 5204 병합 정렬

- 문제 설명 : 병합 정렬을 구현합니다.



## 5205 퀵 정렬

- 문제 설명 : 퀵 정렬을 구현합니다.
- 문제점 : Runtime Error



## 5207 이진 탐색

- 문제 설명 : 이진 탐색 
- 문제점 : 해결 중



## 부분 집합 만들기

```python
# powerset 부분 집합의 합이 10을 만족하는 집합을 모두 구하시오
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]; N = len(arr)
bits = [0] * N
M = 10

# 1. 재귀 함수 호출 + backtrack
def backtrack(k, cur_sum):
    if cur_sum > 10:
        return
    if k == N:
        if cur_sum == M:
            for i in range(N):
                if bits[i]:
                    print(arr[i], end = ' ')
            print()
    else:
        bits[k] = 1
        backtrack(k + 1, cur_sum + arr[k])
        bits[k] = 0
        backtrack(k + 1, cur_sum)

backtrack(0, 0)

print('-'*50)


# 2. 비트 연산
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]; N = len(arr)
bits = [0] * N
for i in range(1, 1 << N):
    result = []
    for j in range(N):
        if i & (1 << j):
            result.append(arr[j])
    if sum(result) == M:
        print(result)
```



## 1486 장훈이의 높은 선반

- 문제 설명 : 

```python
def backtrack(k, cur_sum):
    global result
    if k == N:
        if cur_sum >= M:
            result.add(cur_sum)
    else:
        backtrack(k + 1, cur_sum + arr[k])
        backtrack(k + 1, cur_sum)


T = int(input())
for tc in range(1,T+1):
    N, M = map(int, input().split())
    arr = list(map(int, input().split()))
    result = set()
    
    backtrack(0, 0)
    print('#{} {}'.format(tc, min(result) - M))
```

