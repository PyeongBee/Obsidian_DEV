# Python

### 1. 문자열 뒤집기
```python
S = "abcd"
R = S[::-1]
```

### 2. 빠른 입출력
```PYTHON
import sys
S = sys.stdin.readline().rstrip()
N = int(sys.stdin.readline().rstrip())
```

### 3. 2진 탐색
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
