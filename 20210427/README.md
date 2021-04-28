# 2021.04.27.

- **문제 사이트** : 
  - [x] BOJ
    - [x] 13458 시험감독
    - [x] 4963 섬의 개수


- **사용한 알고리즘**
  - 연산
  - 비선형 자료구조 클린코드
    - DFS/BFS
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



## 4963 섬의 개수

```python
def numIsland(self, grid):
    def dfs(i, j):
        # 더 이상 땅이 아닌 경우 종료
        if i < 0 or i >= len(grid) or \
        j < 0 or j >= len(grid[0]) or \
        grid[i][j] != '1':
            return
        
        grid[i][j] = 0:
        # 동서남북 탐색
        dfs(i + 1, j)
        dfs(i - 1, j)
        dfs(i, j + 1)
        dfs(i, j - 1)
        
    count = 0
    for i in range(len(grid)):
        for j in range(len(grid[0])):
            if grid[i][j] == '1':
                dfs(i, j)
                count += 1
                
    return count
```



## 순열

```python
def permute(self, nums):
    results = []
    prev_elements = []
    
    def dfs(elements):
        # 리프 노드일 때 결과 추가
        if len(elements) == 0:
            results.append(prev_elements[:])
            
        # 순열 생성 재귀 호출
        for e in elements:
            next_elements = elements[:]
            next_elements.remove(e)
            
            prev_elements.append(e)
            dfs(next_elements)
            prev_elements.pop()
            
    dfs(nums)
    return results
```



## 조합

```python
def combine(self, n, k):
    results = []
    
    def dfs(elements, start, k):
        if k == 0:
            results.append(elements[:])
        
        for i in range(start, n + 1):
            elements.append(i)
            dfs(elements, i + 1, k - 1)
            elements.pop()
            
    dfs([], 1, k)
    return results
```



## 부분집합

```python
def subset(self, nums):
    result = []
    
    def dfs(index, path):
        result.append(path)
        
        for i in range(index, len(nums)):
            dfs(i + 1, path + [nums[i]])
            
    dfs(0, [])
    return result
```



