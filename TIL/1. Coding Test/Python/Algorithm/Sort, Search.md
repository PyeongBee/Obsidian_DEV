### Sort
#### 1. 기본 정렬
- sort, sorted 모두 **병합 정렬**을 활용한 정렬이다.
- 퀵소트보다는 느리지만, **최악의 경우에도 O(nlogn)을 보장한다.**
```python
nums = [1, 9, 4, 3, 5, 6]
nums.sort() # inplace sort라서 원본 리스트가 변경된다.

print(nums)
# [1, 3, 4, 5, 6, 9]


nums = [1, 9, 4, 3, 5, 6]
nums = nums.sorted() # 정렬된 리스트가 반환된다.

print(nums)
# [1, 3, 4, 5, 6, 9]
```

#### 2. 2중 정렬
```python
# ORDER BY Y, X (Y 정렬, Y 동일할 때 X 정렬)
def ord(xy):
	X, Y = xy.split()

	# x, y 모두 최대 100,000자리 까지
	# ex) 1, 2이면 2000001
	return int(Y)*1000000 + int(X)

XYs = ['1 2', '-1 3', '4 -1', '3 2']
XYs.sort(key = lambda xy: ord(xy))

print(XYs)
# ['4 -1', '1 2', '3 2', '-1 3']
```


### Search
#### 1. 2진 탐색
```PYTHON
def binary_search(L, start, end, target):
	if start > end:
		return -1
	
	mid = (start + end) // 2

	if L[mid] == target:
		return mid
	elif L[mid] < target:
		start = mid + 1
	else:
		end = mid - 1

	return binary_search(L, start, end, target)
```

