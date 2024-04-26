### 1. Combinations
- 조합. 수학 시간 nCr의 그 조합.
- 순서 상관 없이 n개 중에서 r개를 뽑을 때 경우의 수
- ex) `(1, 2)`와 `(2, 1)`은 같은 경우
```python
from itertools import*
A = [1, 2, 3]

print(list(combinations(A, 2)))
# [(1, 2), (1, 3), (2, 3)]
# 3C2 = (3 * 2) / (2 * 1) = 3가지
```

### 2. Permutations
- 순열. 수학 시간 nPr의 그 순열.
- 순서 상관 있게 n개 중에서 r개를 뽑을 때 경우의 수
- ex) `(1, 2)`와 `(2, 1)`은 다른 경우
```python
from itertools import*
A = [1, 2, 3]

print(list(permutations(A, 2)))

# [(1, 2), (1, 3), (2, 1), (2, 3), (3, 1), (3, 2)]
# 3P2 = 3 * 2 = 6가지
```
