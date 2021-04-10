# 2021.04.09.

- **문제 사이트** : 

  - [x] 백준

    - [x] 2644	촌수계산

  - [ ] Programmers

  - [ ] SWEA

    

- **사용한 알고리즘**

  - GRAPH / BFS / TREE




## 2644	촌수계산

- `Tree와 BFS`
- 문제 : 노드간의 촌수를 계산하라
- 컨셉 : 1) 공통조상을 찾고, 1-1) 없다면 -1 리턴, 2) 공통 조상으로부터 노드거리 계산 BFS 방법 이용
- 클래스를 이용한 풀이를 해봅시다.

```python
V = int(input())
n1, n2 = map(int, input().split())
E = int(input())

tree = [[] for _ in range(V + 1)]
for _ in range(E):
    p, c = map(int, input().split())
    tree[p].append(c)
"""i.g.
0 : [],
1 : [2, 3],
2 : [7, 8, 9],
3 : [],
4 : [5, 6],
5 : [],
6 : [],
7 : []
"""

# 공통 조상 찾기
def asc(result, node):
    idx = 1
    while not node in tree[idx]:
        if idx == V:
            return
        idx += 1
    result.append(idx)
    asc(result, idx)

result1 = [n1]
result2 = [n2]
asc(result1, n1)
asc(result2, n2)

same_asc = []
if len(result1) >= len(result2):
    for r1 in result1:
        if r1 in result2:
            same_asc += [r1]
            break
else:
    for r2 in result2:
        if r2 in result1:
            same_asc += [r2]
            break
def subtree(node):
    Q = [node]
    visited = [0] * (V + 1)
    visited[node] = 1
    distance = [0] * (V + 1)

    while Q:
        current = Q.pop(0)
        for w in tree[current]:
            if not visited[w]:
                Q.append(w)
                distance[w] = distance[current] + 1
                visited[w] = 1
    return distance


if not len(same_asc):
    print(-1)
else:
    distance = subtree(same_asc[0])
    print(distance[n1] + distance[n2])
```

