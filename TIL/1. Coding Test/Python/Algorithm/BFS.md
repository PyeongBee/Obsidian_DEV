```python
# N * M 행렬 G
G = [[0] * M for _ in range(N)]

F_CHK = -1 # 무엇으로 체크를 할 것이냐
D = [(-1, 0), (1, 0), (0, -1), (0, 1)] # 상하좌우
def BFS_CHK(r, c):
    global G
    Q = [(r, c)]
    while len(Q) > 0:
        (sr, sc) = Q.pop()
        farm[sr][sc] = F_CHK
        for (dr, dc) in D:
            nr, nc = sr + dr, sc + dc
            if nr < 0 or nc < 0 or nr >= N or nc >= M: continue
            if farm[nr][nc] == 1: Q.append((nr, nc))
```

