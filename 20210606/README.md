## 고득점 Kit :  기능개발, 프린터

- **문제 사이트** : 
  - [ ] 백준
  - [x] Programmers
  - [ ] SWEA
- **난이도**:
  - 레벨 2
- **사용한 알고리즘**
  - stack, queue
- **어려웠던 점**:
  - 오랜만에 문제를 풀어서인지 어색했음
  - 속도나 메모리 측면에서 deque를 import하여 풀어보는 연습을 해봐야 겠다.
- **Reference** :
  - ​
- **etc**:

```python
import math
def solution(progresses, speeds):
    completed_days = []
    N = len(progresses)
    for idx in range(N):
        completed_days.append(int(math.ceil((100 - progresses[idx]) / speeds[idx])))

    cnt = 0
    bigger_num = -1
    result = []
    for i, day in enumerate(completed_days):
        if bigger_num <= day:
            bigger_num = day
            result += [cnt]
            cnt = 1
        else:
            cnt += 1

        if i == (N - 1):
            result += [cnt]

    return result[1:]

```

```python
def solution(priorities, location):
    cnt = 1
    while priorities:
        max_num = max(priorities)
        cur_n = priorities.pop(0)
        if max_num > cur_n:
            if location > 0:
                priorities.append(cur_n)
                location -= 1
            else:
                priorities.append(cur_n)
                location += (len(priorities) - 1)

        else: # max_num == cur_n
            if not location:
                return cnt
            else:
                cnt += 1
                location -= 1

```

