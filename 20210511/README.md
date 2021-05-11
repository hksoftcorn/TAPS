# 2021.05.05.

- **문제 사이트** : 
  - [x] Programmers
        - [x] 모의고사
        - [x] 주식가격
        - [x] 체육복


- **사용한 알고리즘**
  - 완전탐색 / 탐욕법 / 스택큐

  ​

## 모의고사

- 문제설명 : 숫자 찍기에 맞추는 숫자 개수를 반환합니다.
- 컨셉 : 브루트포스

```python
def solution(answers):
    answer = [0] * 3

    person1 = [1, 2, 3, 4, 5]                   # 5
    person2 = [2, 1, 2, 3, 2, 4, 2, 5]          # 8
    person3 = [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]    # 10
    i = 0
    while i < len(answers):
        number = answers[i]
        if person1[i % 5] == number:
            answer[0] += 1
        if person2[i % 8] == number:
            answer[1] += 1
        if person3[i % 10] == number:
            answer[2] += 1
        i += 1
    max_cnt = max(answer)

    result = []
    for i in range(3):
        if max_cnt == answer[i]:
            result.append(i+1)
    return result

answers = [1,2,3,4,5]
print(solution(answers))
```



## 주식가격

- 문제 설명 : 초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때, 가격이 떨어지지 않은 기간은 몇 초인지를 return 하도록 solution 함수를 완성하세요.
- 컨셉 : 1) Stack 2) price 가격과 비교하면서 stack에서 꺼내기 3) 배열에 인덱스 더하기

```python
def solution(prices):
    # prices의 길이는 2이상 100000 이하입니다.
    N = len(prices)
    answer = [0] * N
    stack = []

    for i in range(N):
        price = prices[i]

        # stack이 비어있다면 stack에 넣기
        # (i, price)
        if not stack:
            stack.append((i, price))

        else:
            # stack top과 비교하여, price보다 크다면 꺼내기
            while stack and price < stack[-1][1]:
                idx, _ = stack.pop()
                answer[idx] += (i - idx)
            stack += [(i, price)]

    for s in stack:
        idx, _ = s
        answer[idx] = (N - 1 - idx)

    return answer
```



## 체육복

- 문제 설명 : 전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return합니다.

- 컨셉 : 브루트포스

  *문제를 잘 읽자 : 

  - 여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.

```python
def solution(n, lost, reserve):
    answer = n - len(lost)
    # reserves = {i : 1 for i in reserve}
    reserves = [0] * (n + 1)
    for r in reserve:
        if r in lost:
            lost.remove(r)
            answer += 1
            continue
        reserves[r] = 1
    
    for l in lost:
        if reserves[l-1]:
            reserves[l-1] -= 1
            answer += 1
        elif (l+1) <= n and reserves[l+1]:
            reserves[l+1] -= 1
            answer += 1

    return answer

print(solution(5, [2, 4], [1, 3, 5]))
```
