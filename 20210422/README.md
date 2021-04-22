# 2021.04.22.

- **문제 사이트** : 
  - [x] SWEA
    - [ ] 5247 연산
    - [x] 5248 그룹 나누기
    - [x] 5249 최소신장트리
    - [x] 5250 최소비용
    - [ ] 1251 하나로
    - [ ] 5251 최소이동거리
    - [ ] 2814 최장 경로


- **사용한 알고리즘**
  - GRAPH / Heap / Kruskal / Prim / Dijkstra

- 반성 : 무엇을 하고 있나? 어떤 개념을 연습하고 있다거나 확장하고 있다는 느낌이 전혀 없었다. 아직 이론적 토양이 제대로 다져지지 않았기 때문이라고 생각함. 무엇을 연습하고 있는지 다시 돌아보자.



## 5247 연산

- Runtime Error

```python
# Runtime Error
# Hmm,, how can i fix it ?
operations = [1, -1, -10, 2]
def bfs(n):
    global distance
    Q = [n]
    visited = [0] * 1000000
    visited[n] = 1

    while Q:
        cur_n = Q.pop(0)
        if cur_n == M:
            return
        for i in range(4):
            if i == 3:
                next_n = cur_n * operations[i]
            else:
                next_n = cur_n + operations[i]
            if next_n < 0 or next_n >= 1000000: continue
            if not visited[next_n]:
                visited[next_n] = 1
                distance[next_n] = distance[cur_n] + 1
                # if next_n == M:
                #     return
                Q.append(next_n)


T = int(input())
for tc in range(1, T+1):
    N, M = map(int, input().split())
    distance = [0] * 1000000
    bfs(N)
    print('#{} {}'.format(tc, distance[M]))

```



## 5248 그룹 나누기

- 문제 설명 : 1번부터 N번까지의 출석번호가 있고, M 장의 신청서가 제출되었을 때 전체 몇 개의 조가 만들어지는지 반환하시오
- 컨셉 : dfs가 반복된 횟수를 반환합니다.

```python
# dfs가 반복된 횟수를 반환합니다.
def dfs(v):
    global visited
    visited[v] = 1
    
    for w in G[v]:
        if not visited[w]:
            dfs(w)


T = int(input())
for tc in range(1, T+1):
    N, M = map(int, input().split())
    input_data = list(map(int, input().split()))
    G = [[] for _ in range(N + 1)]
    visited = [0] * (N + 1)
    for i in range(M):
        p, c = input_data[2 * i : 2 * (i + 1)]
        G[p].append(c)
        G[c].append(p)

    cnt = 0
    for idx in range(1, N + 1):
        if not visited[idx]:        
            cnt += 1
            dfs(idx)
            
    print('#{} {}'.format(tc, cnt))
```



## 5249 최소신장트리

MST 최소신장트리

- 문제 설명 : 그래프에서 사이클을 제거하고 모든 노드를 포함하는 트리를 구성할 때, 가중치의 합이 최소가 되도록 만드는 최소신장트리를 구하시오
- 컨셉 : Prim's Algorithm

```python
T = int(input())
for tc in range(1,T+1):
    V, E = map(int, input().split()) # V(Vertex): 정점은 0번부터 V까지, E(Edge): 간선의 수
    G = [[] for _ in range(V + 1)]

    for _ in range(E):
        u, v, w = map(int, input().split())
        G[u].append((v, w))
        G[v].append((u, w))
    
    MST = [0] * (V + 1)
    key = [0xfffffff] * (V + 1)
    key[0] = 0
    ans = 0
    
    for _ in range(V + 1): # 0 ~ V 까지 모든 정점을 돌아봅니다.
        u, min_key = 0, 0xfffffff   # 값을 초기화 합니다.
        for i in range(V + 1):
            if not MST[i] and min_key > key[i]:
                u, min_key = i, key[i]
        MST[u] = 1
        ans += key[u]

        for v, w in G[u]:
            if not MST[v] and key[v] > w:
                key[v] = w

    print('#{} {}'.format(tc, ans))

```



## 5250 최소비용

- 문제 설명 : N x N Matrix에서 (0, 0)에서 출발하여 (N-1, N-1)까지 도달하는 최소 비용을 구하시오.
- 컨셉 : Dijkstra Algorithm / (1) 이동마다 cost는 +1 / (2) 기입된 숫자는 높이를 말하며, 낮은 곳에서 높은 곳으로 이동 시에는 높이 차만큼의 cost가 붙음

```python
import sys; sys.stdin = open('sample_input.txt', 'r')


dr = [-1, 1, 0, 0]
dc = [0, 0, -1, 1]
def bfs(r, c):
    Q = [(r, c)]
    visited = [[0] * N for _ in range(N)]
    visited[r][c] = 1
    dist[r][c] = 0
    
    while Q:                                                          # BFS 시작
        cur_r, cur_c = Q.pop(0)                                       # 자료구조 : 큐
        for i in range(4):                                            # 4방향을 돌아다닙니다.
            nr = cur_r + dr[i]
            nc = cur_c + dc[i]
            if 0 > nr or nr >= N or 0 > nc or nc >= N: continue
            # if not visited[nr][nc]:   
            if arr[nr][nc] - arr[cur_r][cur_c] > 0:                   # 경사를 올라간다면 cost를 더해줍니다.
                cost = arr[nr][nc] - arr[cur_r][cur_c] + 1
            else:                                                     # 아니라면 그대로 +1
                cost = 1
            if dist[nr][nc] > dist[cur_r][cur_c] + cost:              # 다음지역과 현재지역 + cost를 비교합니다.
                dist[nr][nc] = dist[cur_r][cur_c] + cost
                visited[nr][nc] = 1
                Q.append((nr, nc))


T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
    s = (0, 0)
    dist = [[0xfffffff] * N for _ in range(N)]
    bfs(*s)
    print('#{} {}'.format(tc, dist[N-1][N-1]))
```



## 1251 하나로

- 
- 



## 5251 최소이동거리

- 
- 



## 2814 최장 경로

- 

