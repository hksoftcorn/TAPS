
## 72414 :  광고삽입

- **문제 사이트** : 
  - [ ] 백준
  - [x] Programmers
  - [ ] SWEA
- **난이도**:
  - 레벨 3
- **사용한 알고리즘**
  - 구현?
- **어려웠던 점**:
  - 시간초과
  - 풀어가면서 점점 뭔가 잘못되어가는 거를 느겼다...
- **Reference** :
  - https://programmers.co.kr/learn/courses/30/lessons/72414/solution_groups?language=python3
- **etc**:




`reference : 윤응구.py`

- 새롭게 배운 점
  - lambda 표현식
  - := 대입표현식, 연산 표현식에 이름을 부여하고 재사용할 수 있도록함, 이는 python 3.8부터 적용.
  - zip 사용의 유연함
- 문제풀이 개념에서 배운 점
  - 시작점과 끝점을 활용한 배열의 수 표현이 우아하다
  - zip을 활용한 양끝점 비교를 통한 수비교도 차근차근 살펴볼만하다..
  - 00:00:00 형태로 출력하고 싶었는데.. -> f"{mi//3600:02d}:{mi%3600//60:02d}:{mi%60:02d}"




```python
def solution(play, adv, logs):
    c = lambda t: int(t[0:2]) * 3600 + int(t[3:5]) * 60 + int(t[6:8])
    play, adv = c(play), c(adv)
    logs = sorted([s for t in logs for s in [(c(t[:8]), 1), (c(t[9:]), 0)]])
    print(logs)

    v, p, b = 0, 0, [0] * play
    for t, m in logs:
        if v > 0:
            b[p:t] = [v] * (t - p)
        v, p = v + (1 if m else -1), t

    mv, mi = (s := sum(b[:adv]), 0)
    print(mv, mi)
    for i, j in zip(range(play - adv), range(adv, play)):
        s += b[j] - b[i]
        if s > mv:
            mv, mi = s, i + 1

    return f"{mi//3600:02d}:{mi%3600//60:02d}:{mi%60:02d}"

play = "02:03:55"
adv = "00:14:15"
logs = ["01:20:15-01:45:14", "00:40:31-01:00:00", "00:25:50-00:48:29", "01:30:59-01:53:29", "01:37:44-02:02:30"]
print(solution(play, adv, logs)) 
```

