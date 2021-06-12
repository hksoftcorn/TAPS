# 2021.06.12.

- **문제 사이트** : 
  - [x] JUNGOL
    - [x] 2817 로또


- **사용한 알고리즘**
  
  - 조합 combination
  
  

## 2817 로또

```
수의 개수 K와 K개의 수가 주어질 때 가능한 로또 번호를 출력하는 프로그램을 작성하시오.
```

```python
def solution():
    input_data = list(map(int, input().split()))
    n = input_data[0]
    numbers = input_data[1:]
    arr = [0] * 6
    visited = [0] * 50

    def comb(level, k):
        if level == 6:
            print(' '.join(map(str, arr)))
            return

        for i in range(k, n):
            number = numbers[i]
            if visited[number]: continue
            visited[number] = 1
            arr[level] = number
            comb(level + 1, i)
            visited[number] = 0
            
    comb(0, 0)

solution()
```

