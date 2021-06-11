# 2021.06.11.

- **문제 사이트** : 
  - [x] JUNGOL
    - [x] 1490 다음 조합
    - [x] 1997 떡먹는 호랑이


- **사용한 알고리즘**
  
  - 조합
  - 피보나치
  
  

## 1490 다음 조합

```
"""
1부터 N까지의 N개의 정수 중에서 K개를 뽑아낼 때 가능한 경우들을 조합이라고 한다.
예를 들어 N=5고 K=3일 경우 가능한 모든 조합은 다음과 같다

1 2 3
1 2 4
1 2 5
1 3 4
1 3 5
1 4 5
2 3 4
2 3 5
2 4 5
3 4 5

[ 1 2 3 ] 과 [ 3 1 2 ] 와 같이 순서는 다르나 뽑힌수가 같은 경우는 한가지로 간주한다.
다시 말해서 뽑힌 순서는 고려하지 않는다는 것이다.

N과 K가 입력되고 N과 K에서 가능한 조합 중 하나가 입력될 경우, 
조합들을 오름차순으로 정렬 했을 때 다음으로 나오는 조합을 출력하는 프로그램을 작성하라.
"""
```

```python
FLAG = False
idx = 0
found = 0
def solution():
    N, K = map(int, input().split())
    input_data = input()
    arr = [0] * K
    visited = [0] * (N + 1)
    result = []

    def comb(level, k):
        global FLAG, idx, found
        if level == K:
            ans = ' '.join(map(str, arr))
            result.append(ans)
            if ans == input_data:
                FLAG = True
                found = idx
            idx += 1
            return

        for i in range(k, N + 1):
            if visited[i]: continue
            visited[i] = 1
            arr[level] = i
            comb(level + 1, i)
            visited[i] = 0
    comb(0, 1)
    print(result[found + 1] if FLAG and found < (idx - 1) else 'NONE')

solution()

```



## 1997 떡먹는 호랑이

```python
arr = [0] * 31
arr[0] = 1
arr[1] = 1
arr[2] = 2
idx = 3
while idx < 31:
    arr[idx] = arr[idx-1] + arr[idx-2]
    idx += 1

def solution():
    D, K = map(int, input().split())
    # arr[D-2] * Day2 + arr[D-3] * Day1
    a = arr[D-3]
    b = arr[D-2]
    for i in range(1, a):
        if (K - (a * i) ) % b == 0:
            print(i)
            print((K - (a * i) ) // b)
            return
            
solution()
```
