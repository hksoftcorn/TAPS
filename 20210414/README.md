# 2021.04.14.

- **문제 사이트** : 

  - [ ] 백준

  - [ ] Programmers

  - [x] SWEA

    - [x] 11454 babygin
    - [ ] 1244 최대 상금
    - [x] 1247 최적 경로

    

- **사용한 알고리즘**

  - 완전검색 / 백트래킹 / DP

- 순열의 표현에 대해서 알아봅니다.

  - 순열과 조합



## 순열 

- 반복문으로 구현합니다.
- 재귀호출로 구현합니다.

```python
# 1. for문
arr = ['A', 'B', 'C', 'D']
N = len(arr)

for i in range(0, N):
    arr[0], arr[i] = arr[i], arr[0]
    
    for j in range(1, N):
        arr[1], arr[i] = arr[i], arr[1]

        for k in range(2, N):
        	arr[2], arr[k] = arr[k], arr[2]
		    print(arr) # 바꾼 상태를 출력하고
	        arr[2], arr[k] = arr[k], arr[2]
            
        arr[1], arr[i] = arr[i], arr[1]
	    
    arr[0], arr[i] = arr[i], arr[0] # 원상 복귀!

    
# 2. 재귀호출
def perm(k):		# k: 함수 호출의 높이
    if k == N:
        print(arr)
    else:
        for i in range(k, N):
            arr[k], arr[i] = arr[i], arr[k]
            perm(k + 1)
            arr[k], arr[i] = arr[i], arr[k]

perm(0)
```



## Baby gin

- 문제 설명 : Baby-gin을 만족하는지 판별합니다.
- 컨셉 : 완전탐색 - 순열을 통해 앞에 3장과 뒤에 3장을 판별합니다.

```python
"""
Baby gin Game Rule
 0에서 9사이의 숫자 카드에서 임의로 카드 6장을 뽑을 때
  - 3장의 카드가 연속적인 번호를 갖는 경우 run
  - 3장의 카드가 동일한 번호를 갖는 경우 triplete

가능한 조합
- run 2개
- triplete 2개
- run 1개 triplete 1개
"""

# Baby Gin - permutation (recursion)

# baby gin
arr = [6, 6, 7, 7, 6, 7]
# arr = [0, 5, 4, 0, 6, 0]

# not baby gin
# arr = [1, 2, 4, 7, 8, 3]
# arr = [1, 0, 1, 1, 2, 3]


##############################################
##################기존문제풀이##################
import sys
sys.stdin = open('input.txt')

T = int(input())

for tc in range(1, T+1):
    cards = list(map(int, list(input())))

    counter = [0] * 10
    # 2가 되면 성공
    is_babygin = 0

    for card in cards:
        counter[card] += 1

    idx = 0
    while idx < len(counter):
        # triplet 검증
        if counter[idx] >= 3:
            is_babygin += 1
            counter[idx] -= 3
            continue

        # run 검증
        if idx < 8:
            if counter[idx] and counter[idx+1] and counter[idx+2]:
                is_babygin += 1
                counter[idx] -= 1
                counter[idx+1] -= 1
                counter[idx+2] -= 1
                continue
        idx += 1

    if is_babygin == 2:
        result = 1
    else:
        result = 0

    print('#{} {}'.format(tc, result))


##############################################
##################재귀풀이###################
def check(tree_arr):
    if tree_arr[0] == tree_arr[1] == tree_arr[2]:
        return 1
    if tree_arr[0] == tree_arr[1] -1 == tree_arr[2] - 2:
        return 1
    return 0


def babygin(n, k):
    global found
    if k == n:
        print(arr)
        left = arr[:3]
        right = arr[3:]
        if check(left) + check(right) == 2:
            found = True
            return 
    else:
        for i in range(k ,n):
            arr[k], arr[i] = arr[i], arr[k]
            babygin(n, k + 1)
            arr[k], arr[i] = arr[i], arr[k]
            
found = False
arr = [6, 6, 7, 7, 6, 7]
n = len(arr)
babygin(n, 0)
print(found)
```



## 1244 최대 상금

- 문제 설명 : 숫자판이 주어졌을 때, 자리 바꾸는 횟수에 맞추어 최대 숫자를 만드시오
- 컨셉 : 1) 순열을 이용하려고 했다 2) cnt를 신경써서 visited에 담아준다
- 순열을 이용해서 쉽게 풀리는 줄 알았는데?? 너무 안 풀려서 힌트를 봤지만 이게 뭔가 싶다.
- reference : 방지환's code

```python
import sys; sys.stdin = open('input.txt', 'r')

def solution(c):
    global max_num
    if not c:   # count 횟수가 남지 않았으면
        tmp = int(''.join(arr))
        if max_num < tmp:
            max_num = tmp
        return
    else:
        for i in range(0, n-1):
            for j in range(i + 1, n):
                arr[i], arr[j] = arr[j], arr[i]
                tmp = int(''.join(arr))
                if not visited.get((tmp, c)):
                    visited[(tmp, c)] = True
                    solution(c - 1)
                arr[i], arr[j] = arr[j], arr[i]


T = int(input())

for tc in range(1, T+1):
    N, C = input().split()  # N: 숫자판, C: 자리 바꿈 횟수
    arr = list(N)

    n = len(arr)
    c = int(C)

    visited = {}
    max_num = 0
    solution(c)
    
    print('#{} {}'.format(tc, max_num))



```



## 1247 최적 경로

- 문제 설명 : 10진수를 2진수로 바꾸어 반환합니다.
- 컨셉 : 1) 2로 나누어 몫과 나머지를 구합니다. 2) 나머지를 거꾸로 담으면 이진수가 완성됩니다.

```python
T = int(input())

for tc in range(1, T+1):
    N, M = map(int, input().split())
    # 1. M을 2진수로 바꾸기
    B = []
    while M > 0:
        M, r = divmod(M, 2)
        B.insert(0, r)

    # 2. M의 뒤에서부터 N번째 까지 && 1인지 확인하기
    def check(N):
        for i in range(N):
            if not B or B.pop() != 1:
                return False
        return True
    # 3. True : ON / False : OFF
    print('#{} {}'.format(tc, 'ON' if check(N) else 'OFF'))
```

