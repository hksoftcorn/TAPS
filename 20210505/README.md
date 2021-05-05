# 2021.05.05.

- **문제 사이트** : 
  - [x] Programmers
        - [x] 네트워크
        - [x] 타켓넘버
        - [x] 완주하지 못한 선수
        - [x] 전화번호 목록
        - [x] 가장 먼 노드


- **사용한 알고리즘**
  - BFS / DFS / 해시 / 그래프

  ​

## 네트워크

- 문제설명 : 컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

- 컨셉 : 1) DFS 구현 2) DFS가 돌아가는 횟수 계산

  *주어진 인접행렬은 대칭이 아닙니다...

```python
def solution(n, computers):
    answer = 0
    visitied = [0] * n
    
    def dfs(v):
        visitied[v] = 1
        for i in range(n):
            if not visitied[i] and computers[v][i] == 1:
                dfs(i)

    for i in range(n):
        if not visitied[i]:
            answer += 1
            dfs(i)           

    return answer

print(solution(4, [[0] * 4 for _ in range(4)]))

```



## 타겟넘버

- 문제 설명 : 사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성
- 컨셉 : 1) 순열의 합을 구합니다 2) 순열의 합이 target 숫자와 같은 경우를 구합니다.

```python
# 1) 조합으로 풀기
answer = 0
def solution(numbers, target):
    N = len(numbers)
    bits = [0] * N
    if sum(numbers) < target:
        return 0

    def backtrack(k):
        global answer
        if k == N:
            total = 0
            for i in range(N):
                if bits[i]:
                    total -= numbers[i]
                else:
                    total += numbers[i]
            if total == target:
                answer += 1 

        else:
            bits[k] = 0
            backtrack(k + 1)
            bits[k] = 1
            backtrack(k + 1)

    backtrack(0)
    return answer

```

```python
# 2) deque 활용
from collections import deque

def solution(numbers, target):
    answer = 0
    queue = deque([(0, 0)]) # sum, level
    while queue:
        s, l = queue.popleft()
        if l > len(numbers):
            break
        elif l == len(numbers) and s == target:
            answer += 1
        queue.append((s+numbers[l-1], l+1))
        queue.append((s-numbers[l-1], l+1))

    return answer
```





## 완주하지 못한 선수

- 컨셉 : 해시를 연습합니다.

```python
def solution(participant, completion):
    # sol1
    # for comp in completion:
    #     participant.remove(comp)
    # return participant[0]

    # sol2
    result = {}
    for p in participant:
        result[p] = result.get(p, 0) + 1

    for c in completion:
        result[c] -= 1

    for key, value in result.items():
        if value > 0:
            return key

```



## 전화번호 목록

- 컨셉 : 1) 정렬을 합니다. 2) 비교하는 숫자 뒤의 수가 같지 않다면, 그 뒤의 숫자들도 같지 않습니다.

```python
def solution(phone_book):
    answer = True
    N = len(phone_book)
    phone_book.sort()

    for i in range(0, N - 1):
        number = phone_book[i]
        next_nubmer = phone_book[i + 1]
        if len(number) > len(next_nubmer): continue
        if number == next_nubmer[:len(number)]:
            return False
    return answer

```



## 가장 먼 노드

- 문제 설명 : 가장 먼 노드의 개수를 찾습니다.
- 컨셉 : BFS로 풀었습니다.

```python
def solution(n, edge):
    G = [[] for _ in range(n+1)]
    for e in edge:
        v, u = e
        G[v].append(u)
        G[u].append(v)

    visited = [0] * (n + 1)
    dist = [0] * (n + 1)
    Q = [1]
    visited[1] = 1
    dist[1] = 0
    max_cnt = 0
    while Q:
        cur_n = Q.pop(0)
        if max_cnt < dist[cur_n]:
            max_cnt = dist[cur_n]

        for adj in G[cur_n]:
            if not visited[adj]:
                visited[adj] = 1
                dist[adj] = dist[cur_n] + 1
                Q.append(adj)

    return dist.count(max_cnt)
```

