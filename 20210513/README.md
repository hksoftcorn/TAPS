# 2021.05.13. 

## 월간 코드 챌린지 시즌2 (5월)

- **문제 사이트** : 
  - [x] Programmers
        - [x] 1번 : 약수의 개수
        - [x] 2번 : 비트가 1~2개 다른 수
        - [x] 3번 : "110" 옮기기
        - [x] 4번 : 트리 - 서브트리 + 부모노드 값 바꾸기


- **사용한 알고리즘**
  - 완전탐색 / 정렬 / 이분탐색

  ​

## 1번

- 문제설명 : `left`부터 `right`까지의 모든 수들 중에서, 약수의 개수가 짝수인 수는 더하고, 약수의 개수가 홀수인 수는 뺀 수를 반환
- 컨셉 : 1) 수의 범위가 1000까지, 따라서 31까지 제곱수를 담아줍니다 2) 제곱수가 포함되었다면 total에서 값을 빼줍니다

```python
def solution(left, right):
    odd_list= {i * i for i in range(1, 32)}

    answer = sum(list(range(left, right + 1)))
    for number in range(left, right + 1):
        if number in odd_list:
            answer -= (number * 2)

    return answer
```



## 2번

- 문제 설명 : 양의 정수 x에 대한 함수 f(x)를 다음과 같이 정의합니다.x보다 크고 x와 비트가 1~2개 다른 수들 중에서 제일 작은 수를 반환합니다. i.g. f(2) = 3 // f(7) = 11
- 컨셉 : brute-force... 1) atob 비트 변환 2) 뒤에서부터 비트 다른 갯수 카운트 3) 만약 다른 비트가 1 또는 2개 라면 반환
- 해설 : 

```python

# 9/11 solved (-2 time over)
def solution(numbers):
    answer = []

    def itob(i):
        ans = ''
        while i:
            ans = str(i % 2) + ans
            i //= 2
        return ans

    def find_min_bit(number_bit):
        tmp = number
        while True:
            tmp += 1
            x = itob(tmp)
            cnt = len(x) - length
            for i in range(1, length + 1):
                if number_bit[-1 * i] != x[-1 * i]:
                    cnt += 1
                if cnt > 2:
                    break
            else:
                return tmp

    for number in numbers:
        number_bit = itob(number)
        length = len(number_bit)
        ans = find_min_bit(number_bit)
        answer += [ans]

    return answer

```



## 3번

- 문제 설명 : x에 있는 "110"을 뽑아서, 임의의 위치에 다시 삽입합니다.문자열 중 사전 순으로 가장 앞에 오는 문자열을 배열에 담아 return 하도록 solution 함수를 완성해주세요.

- 컨셉 : 

  ​	1) 뒤에서부터 110찾기

  ​	2) 앞에서부터 111찾기

  ​	3) 앞에서부터 111을 찾는데 만약 마지막 자리가 111이라면 return

- 보강할 점 : KMP인가?? 문자열 알고리즘 공부

```python

# Time Over
# for문을 활용한 탐색은 빠르지 않음
# 그,, 문자열 탐색을 활용해야함...
def solution(s):
    answer = []

    def move_forward(x):
        front = rear = 0
        x = list(x)
        for i in range(len(x) - 2):
            if front and rear:
                break
            # 1. 뒤에서부터 110찾기
            if not rear and x[i * (-1) -1] == '0' and x[i * (-1) -2] == '1' and x[i * (-1) -3] == '1':
                rear = len(x) - 1 - i
            # 2. 앞에서부터 111찾기
            if not front and x[i] == '1' and x[i + 1] == '1' and x[i + 2] == '1':
                front = i + 2

        x[front], x[rear] = x[rear], x[front]
        return ''.join(x)

    def isTripleOne(x):
        for i in range(len(x) - 3):
            if x[i] == '1' and x[i + 1] == '1' and x[i + 2] == '1':
                return 1
        return 0


    for x in s:
        while isTripleOne(x):
            y = move_forward(x)
            if x == y:
                break
            x = y
        answer += [x]

    return answer

```



## 4번

- 문제 설명 : 이 트리의 루트 노드는 1번 노드1번 쿼리: 정수 u가 주어집니다. u번 노드의 서브 트리의 모든 노드의 값의 합을 구해야 합니다. 2번 쿼리: 정수 u, w가 주어집니다. u번 노드의 값을 삭제한 뒤, u번 노드의 부모 노드의 값을 u번 노드로 복사합니다.u번 노드의 부모 노드에 대해 같은 작업을 반복하며 루트노드까지 거슬러 올라갑니다. 마지막으로 루트 노드의 값을 w로 바꿉니다.
- 트리

```python

def solution(values, edges, queries):
    answer = []
    values = values
    V = len(values)
    G = [[] for _ in range(V + 1)]
    parent = [[] for _ in range(V + 1)]
    # parent = [0] * (V + 1)
    for edge in edges:
        v, u = edge
        G[v].append(u)
        parent[u].append(v)
        # parent[u] = v

    def subtree(v):
        visited = [0] * (V + 1)
        visited[v] = 1
        Q = [v]
        total = 0
        while Q:
            cur_v = Q.pop()
            total += values[cur_v - 1]
            for w in G[cur_v]:
                if not visited[w]:
                    visited[w] = 1
                    Q.append(w)
        return total

    def change_parent_node(v, value):
        # 1) 우선은 이진트리라고 가정하고 풀이
        # while parent[v]:
        #     p = parent[v]
        #     values[v - 1] = values[p - 1]
        #     v = p
        # values[0] = value

        # 2) 여러 부모 노드가 존재??
        Q = [v]   # list
        while Q:
            cur_p = Q.pop()
            for p_node in parent[cur_p]:
                values[cur_p - 1] = values[p_node - 1]
                Q.append(p_node)

        values[0] = value

    for query in queries:
        node, w = query
        if w == -1:
            answer.append(subtree(node))
        else:
            change_parent_node(node, w)

    return answer
```

