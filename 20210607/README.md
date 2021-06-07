
## 고득점 Kit :  다리를 지나는 트럭

- **문제 사이트** : 
  - [ ] 백준
  - [x] Programmers
  - [ ] SWEA
- **난이도**:
  - 레벨 2
- **사용한 알고리즘**
  - 스택 / 큐
- **어려웠던 점**:
  - 큐에 [0] 패딩을 넣어주는 접근법을 떠올리기 힘들었음
  - 또한 while 조건을 무엇을 넣어야 할 지 고민되었음
- **Reference** :
  - 다른사람의 풀이 참고..
- **etc**:


```python
def solution(bridge_length, weight, truck_weights):
    queue = [0] * bridge_length
    total_time = 0

    while queue:
        queue.pop(0)
        total_time += 1

        if truck_weights:
            if truck_weights and sum(queue) + truck_weights[0] <= weight:
                queue.append(truck_weights.pop(0))
            else:
                queue.append(0)

    return total_time
```

