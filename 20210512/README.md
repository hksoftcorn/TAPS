# 2021.05.12.

- **문제 사이트** : 
  - [x] Programmers
        - [x] 카펫
        - [x] K번째수
  - [x] BOJ
        - [x] 2343_기타 레슨


- **사용한 알고리즘**
  - 완전탐색 / 정렬 / 이분탐색

  ​

## 카펫

- 문제설명 : 카펫의 가로, 세로 크기를 순서대로 배열에 담아 반환합니다.
- 컨셉 : 브루트포스

```python
def solution(brown, yellow):
    answer = []
    LW = (brown - 4) // 2

    for y in range(1, yellow // 2 + 1):
        q, r = divmod(yellow, y)
        if r == 0:
            if q + y == LW:
                answer.extend([q+2, y+2])
                break
    else:
        answer.extend([LW+1, LW+1])
    return answer
```



## K번째수

- 문제 설명 : 배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 반환합니다.
- 컨셉 : 

```python
def solution(array, commands):
    answer = []
    for command in commands:
        i, j, k = command
        my_arr = array[i-1 : j]
        my_arr.sort()
        answer.append(my_arr[k-1])
    return answer


"""
-파이썬스러운 풀이법-
"""
def solution(array, commands):
    return list(map(lambda x:sorted(array[x[0]-1:x[1]])[x[2]-1], commands))
```



## 2343_기타 레슨

- 문제 설명 : 

  - (1) 블루레이를 녹화할 때, 레슨의 순서가 바뀌면 안된다.
  - (2) 강토는 이 블루레이가 얼마나 팔릴지 아직 알 수 없기 때문에, 블루레이의 개수를 가급적 줄이려고 한다. 
  - (3) 오랜 고민 끝에 강토는 M개의 블루레이에 **모든 기타 레슨 동영상을 녹화하기로 했다.**
  - (4) 이 때, 블루레이의 크기(녹화 가능한 길이)를 최소로 하려고 한다. 단, M개의 블루레이는 모두 같은 크기이어야 한다.
  - (5) 이 때, 가능한 블루레이의 크기 중 최소를 구하는 프로그램을 작성하시오.

- 컨셉 : left : 최소 블루레이 크기 (max of arr) right : 최대 블루레이 크기 (sum of arr) mid : (left + right) // 2 

  ​	1) 만약 블루레이의 개수가 부족하다면 right = mid - 1

  ​	2) 만약 블루레이의 개수가 초과하다면 left = mid + 1

- reference : https://deok2kim.tistory.com/109

```python
import sys; sys.stdin=open('2343.txt', 'r')

N, M = map(int, input().split())
arr = list(map(int, input().split()))

def solution():
    cnt = 0
    total = 0
    for i in range(N):
        if total + arr[i] > mid:
            cnt += 1
            total = 0
        total += arr[i]
    else:
        if total:
            cnt += 1
    return cnt

right = sum(arr)
left = max(arr)
while left <= right:
    mid = (right + left) // 2
    cnt = solution()
    if cnt <= M:
        right = mid - 1
    elif cnt > M:
        left = mid + 1

print(left)
```
