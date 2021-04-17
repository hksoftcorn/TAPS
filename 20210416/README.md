# 2021.04.15.

- **문제 사이트** : 

  - [x] SWEA

    - [x] 5188 최소합
    - [x] 5189 전자카트
    - [x] 5201 컨테이너 운반
    - [x] 5202 화물도크
    - [x] 4366 정식이의 은행업무
    - [x] 2819 격자판의 숫자 이어붙이기
    - [ ] 5203 베이비진 게임

    

- **사용한 알고리즘**

  - 완전검색 / 백트래킹 / DP
  
- 이번주에 풀지 못한 문제들을 해결했습니다.



## 5201 컨테이너 운반

- 문제 설명 : 화물이 실려 있는 N개의 컨테이너를 M대의 트럭으로 A도시에서 B도시로 운반할 때 운반되어진 최대 화물 무게를 구하라
- 컨셉 : 1) 화물과 트럭을 내림차순 정렬 2) 화물을 차례대로 트럭에 담을 수 있는 지 확인 3) 만약 담을 수 있다면 - 다음 화물, 다음 트럭 4) 만약 담을 수 없다면 - 다음 화물로 넘어감 5) cnt에 적재한 화물의 무게를 더합니다.

```python
import sys; sys.stdin = open('sample_input.txt', 'r')

"""
풀이순서
1. 화물과 트럭을 내림차순 정렬
2. 화물을 차례대로 트럭에 담을 수 있는 지 확인
3. 만약 담을 수 있다면 - 다음 화물, 다음 트럭
4. 만약 담을 수 없다면 - 다음 화물로 넘어감
5. cnt에 적재한 화물의 무게를 더합니다.
"""
T = int(input())
for tc in range(1, T+1):
    N, M = map(int, input().split())    # N : 컨테이너 수, M : 트럭 수
    weights = list(map(int, input().split()))   # w : 화물의 무게
    trucks = list(map(int, input().split())) # t : 트럭의 적재용량

    weights.sort(reverse=True)
    trucks.sort(reverse=True)
    cnt = 0

    while len(weights) > 0 and len(trucks) > 0:
        w = weights.pop(0)  # 화물 중 가장 무게운 놈
        for i in range(len(trucks)):
            if w > trucks[i]: continue
            trucks.pop(0)
            cnt += w
            break
    
    print('#{} {}'.format(tc, cnt))
```



## 4366 정식이의 은행업무

- 문제 설명 : 2진수와 3진수에서 1자리씩 바꾸어 올바른 값(10진수)을 추측하시오.
- 컨셉 : 1) 가능한 2진수 경우를 구합니다. 2) 2진수를 10진수로 바꾸어 set에 담습니다. 3) 가능한 3진수 경우를 구합니다. 4) 3진수를 10진수로 바꾸어 set에 담습니다. 5) 두개의 set에서 중복되는 수를 출력합니다.

```python
import sys; sys.stdin = open('sample_input.txt', 'r')
"""
풀이법:
1. 가능한 2진수 경우를 구합니다.
2. 2진수를 10진수로 바꾸어 set에 담습니다.

3. 가능한 3진수 경우를 구합니다.
4. 3진수를 10진수로 바꾸어 set에 담습니다.

5. 두개의 set에서 중복되는 수를 출력합니다.
"""
def change_binary(c): # c: char
    if c == '0':
        return '1'
    else:
        return '0'

def b_to_d(b: str): # b: binary
    ans = 0
    for i in range(n):
        ans += int(b[n -1 - i]) * (2 ** i)
    return ans    

def t_to_d(t: str): # t: ternary
    ans = 0
    for j in range(m):
        ans += int(t[m -1 - j]) * (3 ** j)
    return ans


T = int(input())
for tc in range(1, T+1):
    binary = list(input())
    ternary = list(input())
    n = len(binary)
    m = len(ternary)


    # 1. 가능한 2진수 경우를 구합니다.
    binary_list = []
    for i in range(n):
        b = change_binary(binary[i])
        tmp = binary[:]
        tmp[i] = b
        binary_list.append(tmp)

    # 2. 2진수를 10진수로 바꾸어 set에 담습니다.
    binary_to_decimal = set()
    for bl in binary_list:
        b = ''.join(bl)
        binary_to_decimal.add(b_to_d(b))

    # 3. 가능한 3진수 경우를 구합니다.
    ternary_list = []
    for j in range(m):
        if ternary[j] == '0':
            tmp = ['1', '2']
        elif ternary[j] == '1':
            tmp = ['0', '2']
        else:
            tmp = ['0', '1']

        for t in tmp:
            arr = ternary[:]
            arr[j] = t
            ternary_list.append(arr)

    # 4. 3진수를 10진수로 바꾸어 set에 담습니다.
    ternary_to_decimal = set()
    for tl in ternary_list:
        t = ''.join(tl)
        ternary_to_decimal.add(t_to_d(t))

    result = binary_to_decimal & ternary_to_decimal
    print('#{} {}'.format(tc, *result))
```

##### 다른 풀이법 XOR

```python
def f(b, t):
    # bint = int(b, 2)
    bint = 0
    for x in b:
        bint = bint * 2 + int(x)
    binary = []
    for i in range(len(b)):
        binary.append(bint ^ (1 << i)) # 2진수의 1비트씩을 바꿔서 저장
        
    for i in range(len(t)): # 3진수에서 다른 두 수로 바꿔볼 자리
        num1 = 0
        num2 = 0
        for j in range(len(t)):
            if i != j:
                num1 = num1 * 3 + int(t[j])
                num2 = num2 * 3 + int(t[j])
            else:
                num1 = num1 * 3 + (int(t[j]) + 1) % 3	# 0 -> 1 / 1 -> 2 / 2 -> 0
                num2 = num2 * 3 + (int(t[j]) + 2) % 3	# 0 -> 2 / 1 -> 0 / 2 -> 1
                
        if num1 in binary:
            return num1
        if num2 in binary:
            return num2   

T = int(input())
for tc in range(1 T+1):
    b = input()
    t = input()
    r = f(b, t)
    
```



## 2819 격자판의 숫자 이어 붙이기

- 문제 설명 : 4 x 4 격자판 임의의 시작점에서 6번 이동하여 만들 수 있는 문자열의 개수를 구하시오.
- 컨셉 : 1) 임의의 시작점 출발 2) 상하좌우 이동하면서 matrix 범위안에서 재귀호출 3) 이동 횟수가 6이 되면 만들어진 문자열을 set에 추가 4) 만들어진 set의 길이를 출력합니다.

```python
import sys; sys.stdin = open('sample_input.txt', 'r')

dr = [-1, 1, 0, 0]
dc = [0, 0, -1, 1]
def f(r, c, n, s):
    if n == 7:
        t.add(s)
    else:
        for i in range(4):
            nr = r + dr[i]
            nc = c + dc[i]
            if 0 <= nr < 4 and 0 <= nc < 4:
                f(nr, nc, n + 1, s + str(arr[nr][nc]))
                
T = int(input())
for tc in range(1, T+1):
    arr = [list(map(int, input().split())) for _ in range(4)]
    t = set()
    for r in range(4):
        for c in range(4):
            f(r, c, 0, '')  # r, c : 현재 좌표 / n = 이동횟수 / '' = 문자열
    print('#{} {}'.format(tc, len(t)))
```

