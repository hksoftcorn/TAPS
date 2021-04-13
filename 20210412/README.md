# 2021.04.12.

- **문제 사이트** : 

  - [ ] 백준

  - [ ] Programmers

  - [x] SWEA

    - [x] 폭탄 작전
    - [x] 자손 노드의 개수
    - [ ] 로봇 대회
    - [x] MergeSort 시간복잡도 계산
    
    

- **사용한 알고리즘**

  - GRAPH / BFS / Array / Tree

  


## 폭탄 작전

- `2차원 배열`

- 문제 : 폭탄의 위치(br, bc)에서 폭발범위(bp)만큼의 대각방향에 있는 적군들의 피해 총합을 반환합니다.

- 컨셉 : 1) 폭탄의 위치(br, bc)에서 폭발범위(bp)만큼의 대각방향에 있는 값들을 더합니다. 2) visited를 통해 방문표시를 합니다. 3) 방문하지 않은 matrix의 값만을 더해줍니다.


  ```python
"""
문제 설명 : 폭탄의 위치(br, bc)에서 폭발범위(bp)만큼의 대각방향에 있는 적군들의 피해 총합을 구합니다.
"""


# 좌상, 우상, 좌하, 우하
dr = [-1, -1, 1, 1]
dc = [-1, 1, -1, 1]

# 6. 파라미터로 폭탄의 위치와 폭발범위를 받습니다.
def solution(br, bc, bp):
    """
    폭탄의 위치(br, bc)에서 폭발범위(bp)만큼의 대각방향에 있는 값들을 더합니다.
    visited를 통해 방문표시를 합니다.
    방문하지 않은 matrix의 값만을 더해줍니다.

    :param br: int (폭탄의 r좌표)
    :param bc: int (폭탄의 c좌표)
    :param bp: int (폭발범위)
    :return:
    """
    global ans
    # 7. 현재 폭탄이 떨어진 위치가 방문하지 않았다면
    if visited[br][bc] == 0:
        # ans 에 값을 더해줍니다.
        ans += matrix[br][bc]
        # 현재 위치를 방문표시 합니다.
        visited[br][bc] = 1

    cur_r, cur_c = br, bc
    # 8. 폭발의 범위만큼 움직입니다.
    for p in range(1, bp + 1):
        # 9. 폭발의 범위는 4방향 대각선입니다.
        for i in range(4):
            # 10. 다음 폭발좌표 nr, nc를 구합니다.
            nr = cur_r + (p * dr[i])
            nc = cur_c + (p * dc[i])
            # 11. matrix의 크기를 넘지 않고 방문하지 않았다면
            if 0 <= nr < N and 0 <= nc < N:
                if visited[nr][nc] == 0:
                    # ans 에 값을 더해줍니다.
                    ans += matrix[nr][nc]
                    # 위치를 방문표시 합니다.
                    visited[nr][nc] = 1


T = int(input())

for tc in range(1, T+1):
    # N : 지도크기 N * N
    # M : 폭탄의 수
    N, M = map(int, input().split())
    # 1. N * N matrix을 입력받습니다.
    matrix = [list(map(int, input().split())) for _ in range(N)]
    # 2. 같은 크기의 visited 을 만들어 줍니다.
    visited = [[0] * N for _ in range(N)]

    # 3. 정답으로 반환할 ans를 지정합니다.
    ans = 0
    # 4. 폭탄의 수만큼 for문을 실행합니다.
    for i in range(M):
        # br, bc : 폭탄의 위치, bp : 폭발범위
        br, bc, bp = map(int, input().split())
        # 5. solution 함수를 통해 ans를 구합니다.
        solution(br, bc, bp)

    print('#{} {}'.format(tc, ans))
  ```

  


## 자손 노드의 개수

- `Binary Tree`
- 문제 : 이진 트리에서 N번 노드의 자손 노드 개수를 알아냅니다.
- 컨셉 : 1) tree[node]에서 자손이 있다면, 자손의 수 만큼 for문을 수행합니다. 2) 이때 수행되는 수 만큼 cnt 값을 +1 하게 됩니다. 즉 자손의 수가 됩니다.

```python
"""
문제 설명 : 이진 트리에서 N번 노드의 자손 노드 개수를 알아냅니다.
"""

def solution(node):
    """
    tree[node]에서 자손이 있다면, 자손의 수 만큼 for문을 수행합니다.
    이때 수행되는 수 만큼 cnt 값을 +1 하게 됩니다. 즉 자손의 수가 됩니다.

    :param node:  int (부모 노드 번호)
    :return: None
    """
    global cnt

    children = tree[node]
    for child in children:
        cnt += 1
        solution(child)


T = int(input())

for tc in range(1, T+1):
    # V : 노드 개수, N : N번 노드
    V, N = map(int, input().split())
    tree = [[] for _ in range(V + 1)]
    info = list(map(int, input().split()))

    # 1. V-1 개의 노드 쌍에 대한 정보(info)를 tree에 저장합니다.
    # p : parent, c : child
    for i in range(V - 1):
        p, c = info[i * 2 : (i + 1) * 2]
        # 2. 부모 p노드에 자식 c를 추가합니다.
        tree[p].append(c)

    # 3. 자손 노드의 수를 담을 cnt 변수입니다.
    cnt = 0
    # 4. solution 함수를 통해 자손의 수를 구합니다.
    solution(N)
    print('#{} {}'.format(tc, cnt))
```

## Merge Sort 시간복잡도 계산

```python
# 4.
1) 
T(n) = 2 * T(n / 2) + n

2)
T(n) = 2 * T(n / 2) + n
      = 4 * T(n / 4) + 2 * n
      = 8 * T(n / 8) + 3 * n
...
∴ T(n) = 2^k * T( n / 2^k ) + k * n

- 2^k = n → k = log{2}(n)
- T(1) = 1

T(n) = n * 1 + log{2}(n) * n
T(n) = n * (1 + log{2}(n))

∴ O(n) = n * log{2}(n)
```

