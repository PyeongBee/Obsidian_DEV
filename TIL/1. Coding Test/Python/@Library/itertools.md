### 1. accumulate, 누적합
[참고 블로그](https://deok2kim.tistory.com/95)

```python
from itertools import accumulate

a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

b = list(accumulate(a))
print(b)  # [1, 3, 6, 10, 15, 21, 28, 36, 45, 55]

b = list(accumulate(a, initial=0))
print(b)  # [0, 1, 3, 6, 10, 15, 21, 28, 36, 45, 55]
```

- 값이 누적되어 반환된다.
- for문 만으로도 값을 누적한 리스트를 뽑을 수 있지만 속도면에서 큰 차이가 난다.

### 2. Combinations
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

### 3. Permutations
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
