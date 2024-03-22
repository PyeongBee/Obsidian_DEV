#### 1. key로 value 조회
```python
D = dict({5: 1, 3: 3, 4: 2})

print(D.get(5)) # 1

print(D.get(999, 0)) # 0 -- 찾으려는 값이 없을 때 2번째 값을 출력!
```

#### 2. key:value 조회
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

#### 3. 정렬
```python
D = dict({5: 1, 3: 3, 4: 2})

print(sorted(D))
# [3, 4, 5] -- key들이 정렬된 list가 조회된다.

print(sorted(D.items()))
# [(3, 3), (4, 2), (5, 1)] -- (key, value) 튜플이 정렬된 list가 조회된다.

print(sorted(D.items(), key = lambda x: x[1]))
# [(5, 1), (4, 2), (3, 3)] -- value 기준으로 튜플이 정렬된 list가 조회된다.
```

#### 4. 최소값, 최대값
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

#### 5. index로 value 조회
딕셔너리 values()를 list로 캐스팅
```python
D = dict({5: 1, 3: 3, 4: 2})

print(list(D.values())[0]) # 1
```

