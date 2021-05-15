# 2021.05.15. 

## 월간 코드 챌린지 시즌2 (5월)

- **문제 사이트** : 
  - [x] Programmers
        - [x] 1번 : 약수의 개수와 덧셈
        - [x] 2번 : 2개 이하로 다른 비트
        - [x] 3번 : 110 옮기기
        - [ ] 4번 : 중력작용


- **사용한 알고리즘**
  - 완전탐색 / 비트 / 스택 / 트리

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
- 해설 : 1) 짝수의 경우는 +1 끝 2) 홀수의 경우는 2개의 비트를 반전시키는 방법을 사용 number + 2 ** idx - 2 ** (idx - 1)

```python
def solution(numbers):
    answer = []
    def itob(i):
        ans = ''
        while i:
            ans = str(i % 2) + ans
            i //= 2 
        return ans


    def btoi(b):
        total = 0
        i = 0
        while i < len(b):
            total += int(b[len(b) - 1 - i]) * (2 ** i)
            i += 1

        return total


    def find_answer(number):
        odd_byte = list(itob(number))
        for idx in range(len(odd_byte)):
            if odd_byte[len(odd_byte) - 1 - idx] == '0':
                zero_idx = len(odd_byte) - 1 - idx
                odd_byte[zero_idx] = '1'
                while odd_byte[zero_idx + 1] != '1':
                    zero_idx += 1
                odd_byte[zero_idx + 1] = '0'
                return odd_byte
        else:
            odd_byte[0] = '0'
            odd_byte = ['1'] + odd_byte
            return odd_byte



    for number in numbers:
        if number % 2:
            bit_ans = find_answer(number)
            answer.append(btoi(bit_ans))
        else:
            answer.append(number + 1)

    return answer

print(solution([2,7]))
```

```python
"""
좋은 풀이법
손병현.py
"""

def solution(numbers):
    ans = []

    for n in numbers:
        if n & 1:
            tmp, idx = n, 0
            while tmp > 0 and tmp % 2: 
                tmp//=2
                idx+=1
            ans.append(n + 2**idx - 2**(idx-1))
        else: ans.append(n+1)
    return ans
```



## 3번

- 문제 설명 : x에 있는 "110"을 뽑아서, 임의의 위치에 다시 삽입합니다.문자열 중 사전 순으로 가장 앞에 오는 문자열을 배열에 담아 return 하도록 solution 함수를 완성해주세요.

- 컨셉 : 

  ​	1) 뒤에서부터 110찾기

  ​	2) 앞에서부터 111찾기

  ​	3) 앞에서부터 111을 찾는데 만약 마지막 자리가 111이라면 return

- 해설 : stack을 활용합니다. 1) 첫 번째 n개의 입력값을 순회하면서 110과 111을 찾을 수 있습니다. 2) 111을 찾았다면 앞에 110 * cnt 를 넣어줍니다 3) 111을 못 찾았다면 뒤에 붙여줍니다.

- 보강 : 110을 뺀 나머지 stack에서 마지막의 수가 1이면 110 뒤로 보냅니다. 

```python
def solution(s):
    answer = []

    def moving_110(string):
        stack = []
        cnt = 0
        idx_111 = -1
        string = list(string)
        for idx in range(len(string)):
            ele = string[len(string) - 1 -idx]
            stack.append(ele)
            n = len(stack)
            if n <= 2: continue
            if stack[n-1] == '1' and stack[n-2] == '1' and stack[n-3] == '1':
                idx_111 = len(stack)
            if stack[n-1] == '1' and stack[n-2] == '1' and stack[n-3] == '0':
                cnt += 1
                stack.pop()
                stack.pop()
                stack.pop()
        
        if idx_111 == -1:
            stack = stack[::-1]
            tmp = 0
            while stack and stack[-1] != '0':
                stack.pop()
                tmp += 1
            ans = stack + ['1', '1', '0'] * cnt + ['1'] * tmp
            return ans
        else:
            ans = stack[:idx_111] + ['0', '1', '1'] * cnt + stack[idx_111:]
            return ans[::-1]


    for string in s:
        answer.append(''.join(moving_110(string)))

    return answer

print(solution(["1110","100111100","0111111010"]))
```

```python
"""
박성범.py
"""
def find(x):
    ones = 0
    last_zero_index = 0
    count_110 = 0
    remain = ""
    for i in range(len(x)):
        if x[i] == "0":
            if ones > 1:
                count_110 += 1
                ones -= 2
            else:
                remain += "1"*ones + "0"
                ones = 0
                last_zero_index = i+1
        else:
            ones += 1
    return remain + "110" * count_110 + "1"*ones

def solution(s):
    answer = [find(x) for x in s]
    return answer

```



## 4번

- 문제 설명 : 이 트리의 루트 노드는 1번 노드1번 쿼리: 정수 u가 주어집니다. u번 노드의 서브 트리의 모든 노드의 값의 합을 구해야 합니다. 2번 쿼리: 정수 u, w가 주어집니다. u번 노드의 값을 삭제한 뒤, u번 노드의 부모 노드의 값을 u번 노드로 복사합니다.u번 노드의 부모 노드에 대해 같은 작업을 반복하며 루트노드까지 거슬러 올라갑니다. 마지막으로 루트 노드의 값을 w로 바꿉니다.
- 트리
- 해설 : HLD (Heavy Light Decomposition) 알고리즘 활용
- 세그먼트 트리 또는 Treap 자료구조에 대한 이해..? 잘 모르겠습니당..



