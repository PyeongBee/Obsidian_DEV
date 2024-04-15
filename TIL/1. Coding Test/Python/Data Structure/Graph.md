- 노드 수 N, 간선 수 M을 입력 받을 때 양방향 Graph
- 간선은 set으로 설계했다.
```python
N, M = map(int, input().split())
G = [set() for _ in range(N + 1)]

for _ in range(M):
    A, B = map(int, input().split())
    G[A].add(B)
    G[B].add(A)

print(G)
```