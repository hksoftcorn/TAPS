# 2021.04.08.

- **문제 사이트** : 
  - [x] 백준
    
    - [x] 7465	창용 마을 무리의 개수
    - [x] 2606	바이러스
    - [x] 1260	DFS와 BFS
    - [x] 2178	미로 탐색
  - [ ] Programmers
  - [x] SWEA
    - [x] 1248	공통조상
    - [x] 1219	길찾기
    - [x] 1249	보급로
    - [x] 1226	미로1
  - [x] 1227	미로2
    
    
  
- **사용한 알고리즘**
  
  - GRAPH / DFS / BFS / TREE / BinaryTree




## 7465_창용 마을 무리의 개수

- `2차원 배열과 DFS`
- 배열을 돌면서 DFS를 통해 visit을 채워줍니다.
- 그리고 cnt의 값을 증가시킵니다.



## 1248	공통조상

- `이진 TREE`
- 모든 노드를 while 문을 통해 자식들을 확인해서 부모노드를 찾았다.
  - 더 좋은 방법이 있지 않을까?..
- 서브트리의 개수를 확인할 때 if node: (node 값이 0일 경우 False)가 되는 것을 명심하자



## 1219	길찾기

- `DFS와 BFS 이용`



## 1249	보급로

- `BFS를 이용한 문제`
- 최소 Distance를 구해봅니다. (아래 `2178 미로탐색` 문제 참고)



## 1226	미로1

- `DFS 이용`
- 미로에서는 visit 보다는 지나간 곳을 0으로 바꾸는 것을 추천



## 1227	미로2

- `BFS 이용`
- 미로에서는 visit 보다는 지나간 곳을 0으로 바꾸는 것을 추천
- 시작점이 고정된 값이라는 걸 확인합시다..



## 2606	바이러스

- `DFS를 이용한 문제`

- 고민 : cnt를 어디에 넣어야 할까?

  - 방문하지 않았던 지점을 확인했을 때 cnt를 더해주면 된다!

  

## 1260	DFS와 BFS

- `DFS와  BFS를 이용한 문제`
- 인접 노드 중에서 작은 것부터 선택하여 경로를 나아감
  - 이는 sorted() 함수를 이용하여 해결함
- BFS에서 visit 설정을 하지 않아서 Recursion Error를 마주했다.



## 2178	미로 탐색

- `BFS를 이용한 문제`
- 최소 DIstance를 구하기 위해서 큰 수들로 초기화를 해야함
  - 미래 위치의 값 > 현재까지 값 + 현재 위치 값 이라면 값을 (작은 수로) 바꾸어줍니다.
- `if 0 <= nr < N and 0 <= nc < M:`  이 부분이 직관적이라 더 편하게 썼는데
  - `if 0 > nr or N <= nr or 0 > nc or M <= nc: continue` 이렇게 두면 연산량이 더 줄어드나?

```python
"""
0 : 이동불가
1 : 통로
(1, 1) : 시작점
(N, M) : 도착점
"""
N, M = map(int, input().split())
maze = [list(map(int, input())) for _ in range(N)]
s = (0, 0)

dr = [-1, 1, 0, 0]
dc = [0, 0, -1, 1]
cnt = 0

def bfs(s):
    global cnt
    Q = [s]
    D = [[0xfffffff] * M for _ in range(N)]
    D[s[0]][s[1]] = 1

    while Q:
        r, c = Q.pop(0)

        for i in range(4):
            nr = r + dr[i]
            nc = c + dc[i]
            # if 0 <= nr < N and 0 <= nc < M:
            if 0 > nr or N <= nr or 0 > nc or M <= nc: continue
            if D[nr][nc] > D[r][c] + maze[r][c]:
                D[nr][nc] = D[r][c] + maze[r][c]
                if maze[nr][nc] == 1:
                    Q.append((nr, nc))

    return D[N-1][M-1]

print(bfs(s))
```

