# 2021.04.21.

- **문제 사이트** : 
  - [x] BOJ
    - [x] 1697 숨바꼭질
  - [x] SWEA
    - [x] 2806 N-queens
    - [x] 1865 동철이의 일분배
    - [ ] 2814 최장 경로


- **사용한 알고리즘**
  - 분할 정복 / 백트래킹 / DFS / BFS



## 2806 N-queens

- 문제 설명 : N*N 보드에 N개의 퀸을 서로 다른 두 퀸이 공격하지 못하게 놓는 경우의 수는 몇가지가 있을까?
- 컨셉 : 1) queen이 갈 수 없는 곳들을 찾아봅시다!! 

```python
def is_promising(v):
    global row
    for i in range(v):
        if row[v] == row[i] or abs(row[v]-row[i]) == v - i:
            return False
    return True


def dfs(v):
    global cnt, row, N
    if v == N:
        cnt += 1
    else:
        for i in range(N):
            row[v] = i
            if is_promising(v):
                dfs(v+1)


T = int(input())
for tc in range(1, T+1):
    N = int(input())
    cnt = 0
    row = [0] * N
    dfs(0)
    print(f'#{tc} {cnt}')

```



## 1865 동철이의 일분배

- 문제 설명 : 문제 설명 :  “주어진 일이 모두 성공할 확률”의 최댓값을 구하시오
- 컨셉 : 컨셉 : 5209 최소생산비용 참고. 1) dfs로 풀이 2) 현재 값이 max_percent보다 같거나 낮으면 유망하지 않음, 즉 prunning(가지치기)를 통해 더이상 진행 x
- GENIUS IDEA : 1) worker의 가장 높은 확률을 뽑아둡니다 2) 현재 확률에서 가장 높은 확률을 multiply 하였는데도 현재 percentage보다 낮다면 return 3) 결론적으로 4초 대의 엄청 빠른 속도를 얻을 수 있습니다!

```python
import sys; sys.stdin = open('input.txt', 'r')


def perm(k, percentage):
    if k == N:
        maximum = percentage
    else:
        if percentage <= maximum:
            
        for i in range(k, N):
            schedules[i], schedules[k] = schedules[k], schedules[i]
            cur_percentage = percentage * workers[k][schedules[k]]
            if cur_percentage > maximum:
                perm(k + 1, cur_percentage)
            schedules[i], schedules[k] = schedules[k], schedules[i]      

T = int(input())
for tc in range(1, T+1):
    # 사람의 수
    N = int(input())
    # workers = [[] for _ in range(N)]
    # 함수 정의 (1)
    def string_to_percentage(s):
        return int(s) / 100
    workers = list(map(string_to_percentage, input().split()))
    # 함수 정의 (2) : lambda
    workers = list(map(lambda x: int(x) / 100, input().split()))
    schedule = list(range(N))    
    maximum = 0
    perm(0, 0)
```

```python
# reference : 이세라.py 갓세라님의 코드 참고

def assign(task, percent):
    global result, selected

    # 3-1. 현재까지 계산한 확률에 (예상) 최대 확률을 곱한 값이 result보다 작으면 가망이 없으므로 return
    if result >= percent * possible_max[task]:
        return

    # 3-2. 끝까지 계산했다면, 최댓값이므로 저장
    if task == n:
        result = percent
        return

    for idx in range(n):
        if not selected[idx]:
            selected[idx] = 1
            assign(task + 1, percent * success[task][idx])
            selected[idx] = 0


T = int(input())
for tc in range(1, T + 1):
    # 1-1. input 받기
    n = int(input())
    success = [list(map(lambda x: int(x) / 100, input().split())) for _ in range(n)]

    # 1-2. 필요한 변수 초기화
    result = 0
    selected = [0] * n

    # [KEY] 해당 단계에서 가능한 최대 확률(?)을 미리 구해놓는다.
    # 2-1. 각각의 직원이 성공할 최대 확률을 뽑고
    possible_max = [max(success[x]) for x in range(n)] + [1]
    # 2-2. 해당 단계에서 남은 직원들의 확률을 모두 계산했을 때, 얻을 수 있는 최대 확률을 저장 
    for i in range(n-2, -1, -1):
        possible_max[i] *= possible_max[i+1]
        
    assign(0, 1)
    
    # 4. 결과값 백분율로 바꾸고, 소수점 6자리까지 출력
    print('#{} {:6f}'.format(tc, result * 100))

```



## 1697 숨바꼭질

- 문제 설명 : 위치가 X일 때 1초 후에 X-1 또는 X+1 또는 2*X의 위치로 이동하게 된다. Y와 만나는 가장 빠른 시간을 구하시오.
- 컨셉 : 1) BFS 활용 2) dist 배열을 활용해서 거리 찾기 3) dijkstra 알고리즘이 이런거랑 비슷한가??

```python
move = [1, -1, 2]
def bfs(n):
    global cnt, dist
    visited = [0] * 100001
    
    Q = [n]
    visited[n] = 1
    while Q:
        cur_n = Q.pop(0)
        if cur_n == M:
            return
        for i in range(3):
            if i == 2:
                next_n = cur_n * move[i]
            else:
                next_n = cur_n + move[i]
            if 0 > next_n or next_n >= 100001: continue
            if not visited[next_n]:
                visited[next_n] = 1
                dist[next_n] = dist[cur_n] + 1
                Q.append(next_n)

N, M = map(int, input().split())
dist = [0] * 100001
bfs(N)
print(dist[M])
```
