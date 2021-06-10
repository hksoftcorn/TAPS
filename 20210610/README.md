# 2021.06.10.

- **문제 사이트** : 
  - [x] JUNGOL
    - [x] 3106 진법 변환
    - [x] 2814 이진수


- **사용한 알고리즘**
  - 진법
  
  

## 1169 주사위 던지기1

```
A진법 수 N을 입력 받아 B진법 수로 출력하는 프로그램을 작성하시오.

N에 사용되는 값은 0 ~ 9, A ~ Z이다.

(2 ≤ A, B ≤ 36) ( 0≤ N≤ 263-1 )


입력은 100개 이하의 테스트 케이스가 행으로 구분하여 주어진다.
테스트 케이스의 끝에는 0이 주어진다. 
각 테스트 케이스에는 세 수 A, N, B가 공백으로 구분되어 주어진다.
```

```
2 11010 8
32
2 10110 10
22
10 2543 16
9EF
16 ABC 8
5274
0
```

```python
def xToDecimal(x : int, numbers : list) -> int:
    ten = 0
    for i in range(len(numbers)):
        if numbers[i].isdigit():
            ten = x * ten + int(numbers[i])
        else:
            ten = x * ten + ord(numbers[i]) - 55
    return ten

def yFromDecimal(y : int, ten : int) -> str:
    n = ten
    ans = ''
    while n:
        q, r = divmod(n, y)
        if r >= 10:
            ans = chr(r + 55) + ans
        else:
            ans = str(r) + ans
        n = q
    return ans

def solution():
    while 1:
        input_data = list(input().split())
        if len(input_data) == 1:
            return
        n, numbers, m = input_data
        ten = xToDecimal(int(n), numbers)
        ans = yFromDecimal(int(m), ten)
        print(ans if len(ans) else 0)

solution()
```



## 2814 이진수

```python
def binaryToDecimal():
    binary = str(input())
    decimal = 0
    for i in range(len(binary)):
        decimal = 2 * decimal + int(binary[i])
    print(decimal)

binaryToDecimal()
```
