
## 고득점 Kit :  여행경로

- **문제 사이트** : 
  - [ ] 백준
  - [x] Programmers
  - [ ] SWEA
- **난이도**:
  - 레벨 3
- **사용한 알고리즘**
  - dfs
- **어려웠던 점**:
  - 그냥 dfs를 사용하기에는 생각보다 까다로웠음
  - 딕셔너리의 get를 잘 활용하자
  - 마지막에 경로를 뒤집어서 반환한다는 아이디어를 떠올리기가 어려웠음
- **Reference** :
  - ​
- **etc**:


```python
def solution(tickets):
    answer = []
    trips = {}
    for ticket in tickets:
        departure, destination = ticket
        trips[departure] = trips.get(departure, []) + [destination]
    
    trips = {key : sorted(trips[key]) for key in trips.keys()}
    
    def dfs(v):
        while trips.get(v, 0):
            dfs(trips[v].pop(0))
        answer.append(v)
    
    dfs("ICN")
    return answer[::-1]


    # def travel(v):
    #     cur_v = v
    #     while trips.get(cur_v, 0):
    #         next_v = trips[cur_v].pop(0)
    #         answer.append(next_v)
    #         cur_v = next_v

    # def dfs(v):
    #     Q = [v]
    #     if trips.get(v, 0):
    #         next_v = trips[v].pop(0)
    #         answer.append(next_v)
    #         dfs(next_v)

sample2= [["ICN", "SFO"], ["ICN", "ATL"], ["SFO", "ATL"], ["ATL", "ICN"], ["ATL","SFO"]]
print(solution(sample2))
```

