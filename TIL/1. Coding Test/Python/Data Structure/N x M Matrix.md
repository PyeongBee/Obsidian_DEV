### 1. 최소값, 최대값 찾기
#### 1-1. for문을 이용한 단순한 방법
```python
N, M = 1000, 1000
MATRIX = [[0 for _ in range(M)] for _ in range(N)]
MAX = -1

for i in range(N):
	for j in range(M):
		MAX = max(MAX, MATRIX[i][j])
```
- iter = 50 평균 성능 : 589ms
#### **1-2. map 활용**
```python
N, M = 1000, 1000
MATRIX = [[0 for _ in range(M)] for _ in range(N)]
MAX = -1

MAX = max(map(max, MATRIX))
```
- iter = 50 평균 성능 : 93ms