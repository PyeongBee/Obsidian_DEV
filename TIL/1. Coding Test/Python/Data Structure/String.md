### 1. 숫자 각 자리의 합
```python
I = 245

ans = sum(map(int, str(I)))
print(ans)
```

### 2. 입력이 문자인지 숫자인지 확인
```python
S = input()
print(S.isdigit())

# "5" => True
# "haha" => False
```