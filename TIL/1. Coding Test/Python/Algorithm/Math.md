### 1. 소수 판별
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

### 2. 유클리드 호제법 (최대공약수, 최소공배수)
```python
def GCD(x, y):
	while y != 0:
		x, y = y, x%y
	return x

def LCM(x, y):
	return (x * y) // GCD(x, y)
```

### 3. 이항계수, 조합 경우의 수
- n개에서 r개를 뽑는 조합 = nCr
```python
import math
F = math.factorial

def nCr(n, r):
    return int(F(n)/(F(r) * F(n-r)))

n, r = map(int, input().split())

print(nCr(n, r))
```