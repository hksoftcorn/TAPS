# 2021.04.13.

- **문제 사이트** : 

  - [ ] 백준

  - [ ] Programmers

  - [x] SWEA

    - [x] 5185 이진수
    - [ ] 5186 이진수2
    - [x] 10726 이진수 표현
    - [ ] 3752 가능한 시험점수
    - [ ] 1242 암호코드 스캔

    

- **사용한 알고리즘**

  - Binary / Octal / Decimal / Hexadecimal number

- 반성 : binary 변환을 잘 모르겠다.. homework에서 꽉막혔다.. 메모리 초과에,, 문제가 안 풀린다.. ㅠㅠ 

  

## 5185 이진수

- 문제 설명 : 16진수를 2진수로 바꾸어 반환합니다.
- 컨셉 : 1) 아스키 문자로 받아 숫자를 판별합니다. 2) 16진수 자리에 맞게 코드를 반환합니다.

```python
asc = [[0, 0, 0, 0],  #2진법 - 0(16진법)
       [0, 0, 0, 1],  #2진법 - 1(16진법)
       [0, 0, 1, 0],  #2진법 - 2(16진법)
       [0, 0, 1, 1],  #2진법 - 3(16진법)
       [0, 1, 0, 0],  #2진법 - 4(16진법)
       [0, 1, 0, 1],  #2진법 - 5(16진법)
       [0, 1, 1, 0],  #2진법 - 6(16진법)
       [0, 1, 1, 1],  #2진법 - 7(16진법)
       [1, 0, 0, 0],  #2진법 - 8(16진법)
       [1, 0, 0, 1],  #2진법 - 9(16진법)
       [1, 0, 1, 0],  #2진법 - A(16진법) - 10
       [1, 0, 1, 1],  #2진법 - B(16진법) - 11
       [1, 1, 0, 0],  #2진법 - C(16진법) - 12
       [1, 1, 0, 1],  #2진법 - D(16진법) - 13
       [1, 1, 1, 0],  #2진법 - E(16진법) - 14
       [1, 1, 1, 1]]  #2진법 - F(16진법) - 15

# ASCII -> Hexadecimal
def aToh(c):
    # 9이하이면
    if c <= '9':
        return ord(c) - ord('0')
    # 10이상이면
    else:
        return ord(c) - ord('A') + 10

def makeT(x):
    for i in range(4):
        t.append(asc[x][i])

T = int(input())
for tc in range(1, T+1):
    t = []
    _, arr = input().split()
    for i in range(len(arr)):
        makeT(aToh(arr[i]))

    print('#{} {}'.format(tc, ''.join(map(str, t))))

```

## 10726 이진수표현

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

