# 2021.04.28.

- **문제 사이트** : 
  - [x] BOJ
        - [x] 5014 스타트링크
        - [ ] 2573 빙산
        - [ ] 14503 로봇 청소기
        - [ ] 9205 맥주 마시면서 걸어가기


- **사용한 알고리즘**
  - BFS / DFS / 구현

## 5014 스타트링크

- 문제 설명 : S층에서 G층으로 가기 위해 눌러야 하는 버튼의 수의 최솟값을 출력한다. 만약, 엘리베이터로 이동할 수 없을 때는 "use the stairs"를 출력한다.
- 컨셉 : BFS

```python
"""
S층에서 G층으로 가기 위해 눌러야 하는 버튼의 수의 최솟값을 출력한다. 만약, 엘리베이터로 이동할 수 없을 때는 "use the stairs"를 출력한다.

F : 가장 높은 층
S : 시작 층
G : 도착 층
U : 올라갈 수 있는 층높이
D : 내려갈 수 있는 층높이
"""

F, S, G, U, D = map(int, input().split())

def bfs():
    visited = [0] * (F + 1)
    visited[S] = 1
    Q = [S]
    while Q:
        cur_floor = Q.pop(0)
        if cur_floor == G:
            return visited[cur_floor] - 1
        for next_floor in [cur_floor + U, cur_floor - D]:
            if 1<= next_floor <= F:
                if not visited[next_floor]:
                    visited[next_floor] = visited[cur_floor] + 1
                    Q.append(next_floor)
    return -1
result = bfs()
print(result if result != -1 else 'use the stairs')

```

