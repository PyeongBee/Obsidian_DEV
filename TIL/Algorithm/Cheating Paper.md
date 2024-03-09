# Python

### 1. 빠른 입력
```PYTHON
import sys
S = sys.stdin.readline().rstrip()
N = int(sys.stdin.readline().rstrip())
```

### 2. 2진 탐색
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

### 3. 배열 컨트롤
#### 4-1. index 요소 제거
```python
del _list[i]
```

#### 4-2. 배열 정렬 여부 확인
```python
_list == _list.sorted()
```

#### 4-3. 배열 뒤집기
```python
_list = _list[::-1]
```

#### 4-4. 배열 정렬
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

#### 4-5. 배열 -> 문자열 변환 : **구분자.join(리스트)**
```python
_list = [5, 3, 1, 7]
print(" ".join(_list)) # '5 3 1 7'
print(",".join(_list)) # '5,3,1,7'
```