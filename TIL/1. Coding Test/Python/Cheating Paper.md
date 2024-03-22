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

### 2. 데이터가 쌍으로 움직일 때 꿀팁
```python
N = int(input())
mans = [input().rstrip() for _ in range(N)] # ["21 john", "21 mark", "20 hans"]

mans.sort(key = lambda x: int(x.split()[0])) # 21, 21, 20
###### 개별 연산이 필요한 시점에 split()을 하자.
# 메모리도 적게 들고, 시간도 단축된다.

print("\n".join(mans))
```


### 3. filter
#### 3-1. filter 함수 사용
```python
nums = [3, 5, 4, 8, 9]
nums = list(filter(lambda n: n%2 != 0, nums))

print(nums) # [3, 5, 9]
```

#### 3-2. List Comprehension 사용
```python
nums = [3, 5, 4, 8, 9]
nums = [n for n in nums if n%2 != 0]

print(nums) # [3, 5, 9]
```


### 4. enumerate
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


### 5. 참/거짓 조건문 배열화
- `[거짓일 때 값, 참일 때 값][조건문]`
```python
A = 3

print(['True', -1][A != 3])
# False면 0이라서 0번째 요소, True면 1이라서 1번째 요소
```


