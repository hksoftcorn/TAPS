# 2021.04.15.

- **문제 사이트** : 

  - [x] SWEA

    - [x] 5188 최소합
    - [x] 5189 전자카트
    - [ ] 5201 컨테이너 운반
    - [x] 5202 화물도크
    - [ ] 4366 정식이의 은행업무
    - [ ] 2819 격자판의 숫자 이어붙이기
    - [x] 5203 베이비진 게임

    

- **사용한 알고리즘**

  - 완전검색 / 백트래킹 / DP




## 5188 최소합

- 문제 설명 : 주어진 Matrix에서 시작점(0, 0)에서 출발하여 도착점(N-1, N-1)까지의 합이 최소가 되는 값을 찾으시오
- 컨셉 : 1) BFS 2) Distance 활용

```python
import sys; sys.stdin = open('sample_input.txt', 'r')

dr = [-1, 1, 0, 0]
dc = [0, 0, -1, 1]

def bfs(v):
    Q = [v]
    r, c = v
    visited = [[0] * N for _ in range(N)]
    visited[r][c] = 1
    distance[r][c] = arr[r][c]
    while Q:
        cur_r, cur_c = Q.pop(0)
        for i in range(4):
            nr = cur_r + dr[i]
            nc = cur_c + dc[i]
            # if 0<= nr < N and 0 <= nc < N:
            if 0 > nr or nr >= N or 0 > nc or nc >= N: continue
            if not visited[nr][nc]:
                if distance[nr][nc] > distance[cur_r][cur_c] + arr[nr][nc]:
                    distance[nr][nc] = distance[cur_r][cur_c] + arr[nr][nc]
                    Q.append((nr, nc))


T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
    distance = [[0xfffff] * N for _ in range(N)]
    s = (0, 0)
    bfs(s)
    print('#{} {}'.format(tc, distance[N-1][N-1]))
```



## 5189 전자카트

- 문제 설명 : 사무실(1번)을 시작으로 관리구역(2~)을 거쳐서 다시 사무실로 돌아오는 최소값을 찾이시오
- 컨셉 : 1) 순열 - 시작과 끝은 고정 2) 배열의 표현은 1-2-3-1 은 `[1][2]` -> `[2][3]` -> `[3][1]`으로 진행

```python
import sys; sys.stdin = open('sample_input.txt', 'r')

def dist(pos):
    cnt = 0
    for i in range(1, N + 1):
        r = pos[i-1]
        c = pos[i]
        cnt += arr[r][c]
    return cnt


def perm(k):
    global min_dist
    if k == N:
        # print(pos)
        tmp = dist(pos)
        if min_dist > tmp:
            min_dist = tmp
    else:
        for i in range(k, N):
            pos[k], pos[i] = pos[i], pos[k]
            perm(k + 1)
            pos[k], pos[i] = pos[i], pos[k]
            

T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
    pos = list(range(N)) + [0]
    # print(arr, pos)
    min_dist = 0xfffff
    perm(1)

    print('#{} {}'.format(tc, min_dist))
```



## 5201 화물도크

- 문제 설명 : 작업 시간에 맞는 최대의 스케줄을 계산하시오

- 컨셉 : 1) 끝나는 시간으로 정렬  2) 시작 시간이 끝나는 시간보다 같거나 커야함

  - 두 번째 원소로 정렬

    ```python
    schedules.sort(key=lambda x: x[1])
    ```

- 보완점 : 최대의 스케쥴이 맞는가?? 완전 탐색으로 찾아보는 방법도 고려해야 한다.

```python
import sys; sys.stdin = open('sample_input.txt', 'r')

def solution(arr):
    global cnt
    start = -1
    for i in range(len(arr)):
        s, e = arr[i]
        if start <= s:
            cnt += 1
            start = e
    

T = int(input())
for tc in range(1, T+1):
    N = int(input())
    schedules = []

    for _ in range(N):
        s, e = map(int, input().split())
        schedules.append((s, e))

    schedules.sort(key=lambda x: x[1])
    cnt = 0
    solution(schedules)
    print('#{} {}'.format(tc, cnt))
```

