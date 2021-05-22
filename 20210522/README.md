
## 고득점 Kit :  순위

- **문제 사이트** : 
  - [ ] 백준
  - [x] Programmers
  - [ ] SWEA

- **난이도**:
  - 레벨 3

- **사용한 알고리즘**
  - Graph

- **어려웠던 점**:
  - 딕셔너리 안에 set를 사용하고 싶었는데 불가능,,
  - `from collections import defaultdict`를 활용합니다..

- **Reference** :
  - 다른 사람의 풀이코드를 참고

- 배운 점

  - `from collections import defaultdict`

  - 딕셔너리를 만드는 dict클래스의 서브클래스입니다.

  - 작동하는 방식은 주어진 객체의 기본값을 딕셔너리 초깃값으로 지정할 수 있음

  - 숫자, 리스트, 셋 등으로 초기화 할 수 있습니다. (기본값 0, [], set())

  - ```python
    from collections import defaultdict

    int_dict = defaultdict(int)
    int_dict['key']  # 0 : 기본값
    ```

- **etc**:


```python
"""
선수의 수 n, 경기 결과를 담은 2차원 배열 results가 매개변수로 주어질 때 
정확하게 순위를 매길 수 있는 선수의 수를 return 하도록 solution 함수를 작성해주세요.

딕셔너리 배열 안에 set를 활용하여 선수들의 승부결과를 담습니다.

배운 점 : from collections import defaultdict

"""
from collections import defaultdict
def solution(n, results):
    answer = 0
    win, lose = defaultdict(set), defaultdict(set)
    for result in results:
            lose[result[1]].add(result[0])
            win[result[0]].add(result[1])

    for i in range(1, n + 1):
        for winner in lose[i]: win[winner].update(win[i])
        for loser in win[i]: lose[loser].update(lose[i])

    for i in range(1, n+1):
        if len(win[i]) + len(lose[i]) == n - 1: answer += 1
    return answer

    
# from collections import defaultdict

def solution(n, results):
    answer = 0
    win = {i : set([]) for i in range(1, n + 1)}
    lose = {i : set([]) for i in range(1, n + 1)}
    # win, lose = defaultdict(set), defaultdict(set)
    for result in results:
        w, l = result
        print(w, l)
        if not len(win.get(w)):
            win[w] = win.get(w, {l})
        else:
            win[w].add(l)

        if not lose.get(l, 0):
            lose[l] = lose.get(l, {w})
        else:
            lose[l].add(w)
        # lose[result[1]].add(result[0])
        # win[result[0]].add(result[1])
    print(win)
    print(lose)

    for i in range(1, n + 1):
        for winner in lose[i]: win[winner].update(win[i])
        for loser in win[i]: lose[loser].update(lose[i])

    for i in range(1, n+1):
        if len(win[i]) + len(lose[i]) == n - 1: answer += 1
    return answer

print(solution(5, [[4, 3], [4, 2], [3, 2], [1, 2], [2, 5]]))


# def solution(n, results):
#     G = [[] * (n + 1) for _ in range(n + 1)]
#     parent = [[] * (n + 1) for _ in range(n + 1)]

#     for result in results:
#         v, w = result
#         G[v].append(w)
#         parent[w].append(v)

#     def dfs(v):
#         visited[v] = 1
#         for w in G[v]:
#             if not visited[w]:
#                 dfs(w)

#     player = []
#     for i in range(n + 1):
#         visited = [0] * (n + 1)
#         dfs(i)
#         if (len(parent[i]) + sum(visited)) == n:
#             print(i)
#             player += [i]
        

#     print(cnt)          
```

