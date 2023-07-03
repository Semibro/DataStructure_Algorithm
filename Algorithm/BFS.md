# 너비우선탐색 (BFS)

- 개념

    1. 너비우선탐색은 탐색 시작점의 인접한 정점들을 먼저 모두 탐색 후, 방문했던 정점을 바탕으로 다시 인접한 정점을 탐색하는 방식

    2. 인접한 정점들을 탐색 후, 다시 너비우선탐색을 진행하기 위해 선입선출 형태의 큐를 활용

- 예시

    1. [DFS와 BFS](https://www.acmicpc.net/problem/1260)

    ```Python
    from collections import deque

    N, M, V = map(int, input().split())
    graph_dfs = [[] for _ in range(N+1)]
    graph_bfs = [[] for _ in range(N+1)]
    for _ in range(M):
        v1, v2 = map(int, input().split())
        graph_dfs[v1].append(v2)
        graph_dfs[v2].append(v1)
        graph_bfs[v1].append(v2)
        graph_bfs[v2].append(v1)

    # DFS
    sv = V
    stack = []
    res_dfs = [sv]
    visited = [False] * (N+1)
    visited[sv] = True

    while True:
        for W in sorted(graph_dfs[sv]):
            if not visited[W]:
                visited[W] = True
                stack.append(sv)
                res_dfs.append(W)
                sv = W
                break
        else:
            if stack:
                sv = stack.pop()
            else:
                break

    # BFS
    sb = V
    queue = deque()
    res_bfs = [sb]
    visited_bfs = [False] * (N+1)
    queue.append(sb)
    visited_bfs[sb] = True

    while queue:
        t = queue.popleft()
        for i in sorted(graph_bfs[t]):
            if not visited_bfs[i]:
                visited_bfs[i] = True
                queue.append(i)
                res_bfs.append(i)

    print(*res_dfs)
    print(*res_bfs)
    ```