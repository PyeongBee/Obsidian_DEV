#### 1. index 요소 제거
```python
del L[i]
```

#### 2. 배열 정렬 여부 확인
```python
L == L.sorted()
```

#### 3. 배열 뒤집기
```python
L = L[::-1]
```

#### 4. 배열 정렬
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

#### 5. 배열 -> 문자열 변환 : **구분자.join(리스트)**
```python
L = [5, 3, 1, 7]
print(" ".join(L)) # '5 3 1 7'
print(",".join(L)) # '5,3,1,7'
```

#### 6. 배열에서 특정한 원소들만 제거
```python
L = [1, 3, 5, 1, 4, 5, 3, 8, 9, 7]
remove_set = {3, 5}

L = [n for n in L if n not in remove_set]
print(L)
# [1, 1, 4, 8, 9, 7]
```

#### 7. 배열 원소의 합
- 내가 무슨 짓을 해도 sum()보다 빠르기 쉽지 않다.
```python
L = [1, 2, 3]
print(sum(L)) # 6
```
