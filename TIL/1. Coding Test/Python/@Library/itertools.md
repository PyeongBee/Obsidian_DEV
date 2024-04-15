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

