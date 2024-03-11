# Python

## 기본
### 1. 빠른 입출력
```PYTHON
import sys
S = sys.stdin.readline().rstrip()
N = int(sys.stdin.readline().rstrip())

sys.stdout.write(S + "\n") # sys.stdout.write에는 print와 달리 뒤에 개행문자가 없다.
sys.stdout.write(str(N) + "\n")

# 매번 번거로운 입출력을 쉽게
input = sys.stdin.readline
print = sys.stdout.write
S = input().rstrip()
N = int(input().rstrip())

print(S + "\n")
print(str(N) + "\n")
```

### 2. 배열 컨트롤
#### 2-1. index 요소 제거
```python
del _list[i]
```

#### 2-2. 배열 정렬 여부 확인
```python
_list == _list.sorted()
```

#### 2-3. 배열 뒤집기
```python
_list = _list[::-1]
```

#### 2-4. 배열 정렬
```python
### sort() : 원본 배열 변경
_list = [3, 2, 4, 1]
_list.sort()
print(_list) # [1, 2, 3, 4]

_list = [3, 2, 4, 1]
_list.sort(reverse=True)
print(_list) # [4, 3, 2, 1]

### sorted() : 원본 배열 변경 X
_list = [3, 2, 4, 1]
_list = sorted(_list)
print(_list) # [1, 2, 3, 4]

_list = [3, 2, 4, 1]
_list = sorted(_list, reverse=True)
print(_list) # [4, 3, 2, 1]
```

#### 2-5. 배열 -> 문자열 변환 : **구분자.join(리스트)**
```python
_list = [5, 3, 1, 7]
print(" ".join(_list)) # '5 3 1 7'
print(",".join(_list)) # '5,3,1,7'
```



## 알고리즘
### 1. 2진 탐색
```PYTHON
def binary_search(_list, start, end, target):
	if start > end:
		return -1
	
	mid = (start + end) // 2

	if _list[mid] == target:
		return mid
	elif _list[mid] < target:
		start = mid + 1
	else:
		end = mid - 1

	return binary_search(_list, start, end, target)
```

### 2. 소수 판별
```python
# M까지의 소수 판별
M = int(sys.stdin.readline()[:-1])
primeList = [False, False] + [True for _ in range(2, M + 1)]

for i in range(2, M + 1):
    if !primeList[i]: continue
    
    for pi in range(2, M + 1):
        if i * pi >= len(primeList): break
        primeList[i * pi] = 0
```

### 3. 