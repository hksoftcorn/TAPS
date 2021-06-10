# 2021.06.09.

- **문제 사이트** : 
  - [x] JUNGOL
    - [x] 1169 주사위 던지기1
    - [x] 1175 주사위 던지기2


- **사용한 알고리즘**
  - 재귀



## 1169 주사위 던지기1

```
주사위를 던진 횟수 N과 출력형식 M을 입력 받아서 M의 값에 따라 각각 아래와 같이 출력하는 프로그램을 작성하시오.

M = 1 : 주사위를 N번 던져서 나올 수 있는 모든 경우
M = 2 : 주사위를 N번 던져서 중복이 되는 경우를 제외하고 나올 수 있는 모든 경우
M = 3 : 주사위를 N번 던져서 모두 다른 수가 나올 수 있는 모든 경우
 
\* 중복의 예
1 1 2 와 중복 : 1 2 1, 2 1 1
1 2 3 과 중복 : 1 3 2, 2 1 3, 2 3 1, 3 1 2 


*입력형식
첫 줄에 주사위를 던진 횟수 N(2≤N≤5)과 출력모양 M(1≤M≤3)이 들어온다.
*출력형식
주사위를 던진 횟수 N에 대한 출력모양을 출력한다. 작은 숫자부터 출력한다.
```

```
3 1
1 1 1
1 1 2
1 1 3
1 1 4
1 1 5
1 1 6
1 2 1
…
6 6 6

=========

3 2
1 1 1
1 1 2
…
1 1 6
1 2 2
…
5 6 6
6 6 6

=========

3 3
1 2 3
1 2 4
1 2 5
1 2 6
1 3 2
1 3 4
…
6 5 3
6 5 4
```

```python
def solution():
    n, m = map(int, input().split())
    arr = [0] * n
    def dice1(level):
        if level == n:
            print(' '.join(map(str, arr)))
            return
        for i in range(1, 7):
            arr[level] = i
            dice1(level + 1)
    
    def dice2(level, k):
        if level == n:
            print(' '.join(map(str, arr)))
            return
        else:
            for i in range(k, 7):
                arr[level] = i
                dice2(level + 1, i)

    visited = [0] * 7
    def dice3(level):
        if level == n:
            print(' '.join(map(str, arr)))
            return
        for i in range(1, 7):
            if visited[i]: continue
            visited[i] = 1
            arr[level] = i
            dice3(level + 1)
            visited[i] = 0

    if m == 1:
        dice1(0)
    elif m == 2:
        dice2(0, 1)
    elif m == 3:
        dice3(0)

solution()
```



## 1175 주사위 던지기2

```python
def solution():
    n, m = map(int, input().split())
    arr = [0] * n
    def dice(level, cur_sum):
        if cur_sum > m:
            return
        if level == n:
            if cur_sum == m:
                print(' '.join(map(str, arr)))
            return
        for i in range(1, 7):
            arr[level] = i
            dice(level + 1, cur_sum + i)
    dice(0, 0)

solution()
```

