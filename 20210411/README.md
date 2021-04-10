# 2021.04.11.

- **문제 사이트** : 

  - [x] 백준

    - [x] 2468	안전영역

  - [ ] Programmers

  - [ ] SWEA

    

- **사용한 알고리즘**

  - GRAPH / BFS / Array




## 2468	안전영역

- `2차원 배열과 BFS`

- 문제 : 안전한 영역의 수를 반환하라

- 컨셉 : 1) dfs 혹은 bfs 구현 2) 2차원 배열을 하나씩 지나가면서 visit하지 않았으며 지정한 number 보다 크다면 구현한 bfs 실행 3) 실행을 할 때마다 count 값 +1 4) 가장 큰 count 값 반환

- 배운점 

  - `sys.setrecursionlimit(15000)` 을 통해 재귀의 깊이를 조절할 수 있습니다.

  - (10**6) 만큼 늘렸더니 메모리 문제가 발생했습니다. => 적당히 조절해야 합니다.

    ```python
    import sys
    sys.setrecursionlimit(15000)
    ```

  - dfs 재귀방법보다 bfs 푸는 방법이 더 효율적인가? 고민하게 됩니다.

  - count가 0이 되지는 않습니다. max_count의 값을 1로 지정해두고 count와 비교합니다.

    ```python
    max_cnt = 1
    max_cnt = max(cnt, max_cnt)
    ```

```python
import sys
sys.setrecursionlimit(15000)

N = int(input())

matrix = [list(map(int, input().split())) for _ in range(N)]
min_num = min([min(matrix[i]) for i in range(N)])
max_num = max([max(matrix[i]) for i in range(N)])


dr = [-1, 1, 0 , 0]
dc = [0, 0, -1, 1]
def dfs(r, c):
    visited[r][c] = 1

    for i in range(4):
        nr = r + dr[i]
        nc = c + dc[i]
        # if 0 <= nr < N and 0 <= nc < N:
        if nr < 0 or N <= nr or nc < 0 or N <= nc: continue
        if not visited[nr][nc] and matrix[nr][nc] > num:
            dfs(nr, nc)


def bfs(r, c):
    Q = [(r, c)]
    visited[r][c] = 1

    while Q:
        cur_r, cur_c = Q.pop(0)
        for i in range(4):
            nr = cur_r + dr[i]
            nc = cur_c + dc[i]
            if nr < 0 or N <= nr or nc < 0 or N <= nc: continue
            if not visited[nr][nc] and matrix[nr][nc] > num:
                visited[nr][nc] = 1
                Q.append((nr, nc))    


max_cnt = 1
for num in range(min_num, max_num):
    visited = [[0] * N for _ in range(N)]
    cnt = 0
    for i in range(N):
        for j in range(N):
            if visited[i][j] == 0 and matrix[i][j] > num:
                cnt += 1
                bfs(i, j)
    max_cnt = max(cnt, max_cnt)

print(max_cnt)
```

