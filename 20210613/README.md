# 2021.06.13.

- **문제 사이트** : 
  - [x] JUNGOL
    - [x] 1146 selectionSort
    - [x] 1157 bubbleSort
    - [x] 1158 insertionSort


- **사용한 알고리즘**
  
  - 정렬 Sort
  
  

## 1146 selectionSort

```python
def solution():
    n = int(input())
    arr = list(map(int, input().split()))

    for i in range(n - 1):
        min_idx = i
        for j in range(i + 1, n):
            if arr[min_idx] > arr[j]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
        print(' '.join(map(str, arr)))
    
solution()
```



## 1157 bubbleSort

```python
def solution():
    n = int(input())
    arr = list(map(int, input().split()))

    for i in range(n - 1, 0, -1):
        for j in range(i):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
        print(' '.join(map(str, arr)))
    
solution()
```



## 1158 insertionSort

```python
def solution():
    n = int(input())
    arr = list(map(int, input().split()))

    for i in range(1, n):
        selected_num = arr[i]
        for j in range(i):
            if selected_num < arr[j]:
                arr.insert(j, selected_num)
                arr.pop(i + 1)
                break
        print(' '.join(map(str, arr)))

solution()
```

