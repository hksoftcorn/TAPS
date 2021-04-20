# 2021.04.20.

- **문제 사이트** : 
  - [x] SWEA

    - [ ] 5205 퀵 정렬
    - [ ] 5207 이진 탐색
    - [x] 5208 전기버스2
    - [x] 5209 최소생산비용
    - [x] 1865 동철이의 일분배
    - [ ] 2806 N-queens


- **사용한 알고리즘**
  - 분할 정복 / 백트래킹 



## 5205 퀵 정렬

- 문제 설명 : 퀵 정렬을 구현합니다.
- 문제점 : Runtime Error //// Why 😢



## 5207 이진 탐색

- 문제 설명 : 이진 탐색 
- 문제점 : 해결 중 /// Need more time and effort 🤼‍♂️



## 5208 전기버스2

- 문제 설명 : 정류장과 충전지에 대한 정보가 주어질 때, 목적지에 도착하는데 필요한 최소한의 교환횟수를 출력하는 프로그램을 만드시오.
- 컨셉 : 1) 현재 위치서부터 배터리 충전 최대거리 구함 2) 최대거리서부터 -1씩 하여 backtrack 실행 3) 최소 cnt 를 구합니다.

```python
def backtrack(k):
    global cnt, result

    if k >= N:
        if result > cnt:
            result = cnt
        return

    if result < cnt:
        return

    else:
        battery = input_data[k]
        for i in range(k + battery, k, -1):
            cnt += 1
            backtrack(i)
            cnt -= 1


T = int(input())
for tc in range(1, T+1):
    input_data = list(map(int, input().split()))
    N = input_data[0]
    # M = input_data[1:]
    result = 0xfffff
    cnt = 0
    backtrack(1)
    print('#{} {}'.format(tc, result-1))
```



## 5209 최소생산비용

- 문제 설명 : 각 제품의 공장별 생산비용이 주어질 때 전체 제품의 최소 생산 비용을 계산하시오
- 문제점 : 백트래킹을 제대로 이해하지 못한 상태에서 문제를 접근함. 1) 처음에는 순열을 통해서 솔루션을 찾으려고 했지만, 런타임 에러. 2) 순열이 아닌, DFS에서 즉각즉각 sum을 더해주면서 최소값과 비교를 통해 유망함을 확인함 3) 중요 - visited를 원상복구 시킴

```python
def backtrack(k, cur_sum):
    global min_cost
    if k == N:
        if min_cost > cur_sum:
            min_cost = cur_sum
        return

    if cur_sum > min_cost:
        return

    for i in range(N):
        if not visited[i]:
            visited[i] = 1
            backtrack(k + 1, cur_sum + arr[k][i])
            visited[i] = 0
    

T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
    visited = [0] * N
    # orders = list(range(N))
    min_cost = 0xffffffff
    backtrack(0, 0)
    print('#{} {}'.format(tc, min_cost))
```



## 1865 동철이의 일분배

- 문제 설명 :  “주어진 일이 모두 성공할 확률”의 최댓값을 구하시오
- 컨셉 : 5209 최소생산비용 참고. 1) dfs로 풀이 2) 현재 값이 max_percent보다 같거나 낮으면 유망하지 않음, 즉 prunning(가지치기)를 통해 더이상 진행 x

```python
import sys; sys.stdin = open('input.txt', 'r')

def backtrack(k, cur_mult):
    global max_percent
    if cur_mult <= max_percent:
        return

    if k == N:
        if max_percent < cur_mult:
            max_percent = cur_mult
        return

    else:
        for i in range(N):
            if not visited[i]:
                visited[i] = 1
                backtrack(k + 1, cur_mult * arr[k][i] * 0.01)
                visited[i] = 0


T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
    visited = [0] * N
    max_percent = 0
    backtrack(0, 100)
    print('#{} {:.6f}'.format(tc, max_percent))
```



