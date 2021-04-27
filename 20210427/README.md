# 2021.04.27.

- **문제 사이트** : 
  - [x] BOJ
    - [x] 13458 시험감독


- **사용한 알고리즘**
  - 연산
  - 비선형 자료구조 클린코드
    - DFS
    - BFS
    - 백트래킹
    - 순열
    - 조합




## 13458_시험감독

```python
N = int(input())
A = list(map(int, input().split()))
B, C = map(int, input().split())

def solution():
    cnt = len(A)
    arr = [a - B if a - B > 0 else 0 for a in A]
    for i in range(len(arr)):
        number = arr[i]
        if number:
            cnt += (number // C)
            if number % C:
                cnt += 1
    print(cnt)

solution()

```



## DFS

```python


```

