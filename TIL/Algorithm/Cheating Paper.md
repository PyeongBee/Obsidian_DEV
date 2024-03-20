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
del L[i]
```

#### 2-2. 배열 정렬 여부 확인
```python
L == L.sorted()
```

#### 2-3. 배열 뒤집기
```python
L = L[::-1]
```

#### 2-4. 배열 정렬
```python
### sort() : 원본 배열 변경
L = [3, 2, 4, 1]
L.sort()
print(L) # [1, 2, 3, 4]

L = [3, 2, 4, 1]
L.sort(reverse=True)
print(L) # [4, 3, 2, 1]

### sorted() : 원본 배열 변경 X
L = [3, 2, 4, 1]
L = sorted(L)
print(L) # [1, 2, 3, 4]

L = [3, 2, 4, 1]
L = sorted(L, reverse=True)
print(L) # [4, 3, 2, 1]
```

#### 2-5. 배열 -> 문자열 변환 : **구분자.join(리스트)**
```python
L = [5, 3, 1, 7]
print(" ".join(L)) # '5 3 1 7'
print(",".join(L)) # '5,3,1,7'
```

#### 2-6. 배열에서 특정한 원소들만 제거
```python
L = [1, 3, 5, 1, 4, 5, 3, 8, 9, 7]
remove_set = {3, 5}

L = [n for n in L if n not in remove_set]
print(L)
# [1, 1, 4, 8, 9, 7]
```

#### 2-7. 배열 원소의 합
- 내가 무슨 짓을 해도 sum()보다 빠르기 쉽지 않다.
```python
L = [1, 2, 3]
print(sum(L)) # 6
```


### 3. 딕셔너리 컨트롤
#### 3-1. key로 value 조회
```python
D = dict({5: 1, 3: 3, 4: 2})

print(D.get(5)) # 1

print(D.get(999, 0)) # 0 -- 찾으려는 값이 없을 때 2번째 값을 출력!
```

#### 3-2. key:value 조회
```python
D = dict({5: 1, 3: 3, 4: 2})

print(D)
# {5: 1, 3: 3, 4: 2} -- 딕셔너리 그대로 조회된다.

print(D.items())
# dict_items([(5, 1), (3, 3), (4, 2)]) -- 튜플로 조회된다.

print(D.keys())
# dict_keys([5, 3, 4]) -- key만 조회된다.

print(D.values())
# dict_values([1, 3, 2]) -- value만 조회된다.
```

#### 3-3. 정렬
```python
D = dict({5: 1, 3: 3, 4: 2})

print(sorted(D))
# [3, 4, 5] -- key들이 정렬된 list가 조회된다.

print(sorted(D.items()))
# [(3, 3), (4, 2), (5, 1)] -- (key, value) 튜플이 정렬된 list가 조회된다.

print(sorted(D.items(), key = lambda x: x[1]))
# [(5, 1), (4, 2), (3, 3)] -- value 기준으로 튜플이 정렬된 list가 조회된다.
```

#### 3-4. 최소값, 최대값
**참고)** 정렬도 하고 최소, 최대를 찾아야할 땐 정렬해서 D\[0], D\[-1] 구하는 게 낫다.
```python
D = dict({5: 1, 3: 3, 4: 2})

print(min(D.keys())) # 3
print(max(D.keys())) # 5

print(min(D.values())) # 1
print(max(D.values())) # 3

# key나 value로 구해서 튜플로 반환 받고 싶을 때는 items()를 넘기고, 비교 key를 지정하자.
print(min(D.items(), key = lambda x: x[1]))
# (5, 1)
```

#### 3-5. index로 value 조회
딕셔너리 values()를 list로 캐스팅
```python
D = dict({5: 1, 3: 3, 4: 2})

print(list(D.values())[0]) # 1
```

### 4. 데이터가 쌍으로 움직일 때 꿀팁
```python
N = int(input())
mans = [input().rstrip() for _ in range(N)] # ["21 john", "21 mark", "20 hans"]

mans.sort(key = lambda x: int(x.split()[0])) # 21, 21, 20
###### 개별 연산이 필요한 시점에 split()을 하자.
# 메모리도 적게 들고, 시간도 단축된다.

print("\n".join(mans))
```

### 5. filter
#### 5-1. filter 함수 사용
```python
nums = [3, 5, 4, 8, 9]
nums = list(filter(lambda n: n%2 != 0, nums))

print(nums) # [3, 5, 9]
```

#### 5-2. List Comprehension 사용
```python
nums = [3, 5, 4, 8, 9]
nums = [n for n in nums if n%2 != 0]

print(nums) # [3, 5, 9]
```

### 6. enumerate
String을 입력 받고 foreach 쓰면서도 index 살리고 싶을 때 사용한다.
```python
for i, c in enumerate("abcde"):
	print(f'{i}. {c}')

# 0. a
# 1. b
# 2. c
# 3. d
# 4. e
```


## 알고리즘
### 1. 기본 정렬
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

### 2. 2진 탐색
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

### 3. 소수 판별
```python
# M까지의 소수 판별
M = int(sys.stdin.readline()[:-1])
primeList = [False, False] + [True for _ in range(2, M + 1)]

for i in range(2, M + 1):
    if !primeList[i]: continue
    
    for pi in range(2, M + 1):
        if i * pi >= len(primeList): break
        primeList[i * pi] = False
```

### 4. 유클리드 호제법 (최대공약수, 최소공배수)
```python
def GCD(x, y):
	while y != 0:
		x, y = y, x%y
	return x

def LCM(x, y):
	return (x * y) // GCD(x, y)
```

### 5. 이항계수, 조합 경우의 수
- n개에서 r개를 뽑는 조합 = nCr
```python
n, r = map(int, input().split())

ans = 1
for i in range(1, r + 1):
    ans *= (n + 1 - i) / i

print(ans)
```