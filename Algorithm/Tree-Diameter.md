# 트리의 지름 (Tree Diameter)

- 트리에서 정점 두개를 잡고 거리를 쟀을 때, 가장 거리가 긴 두 정점을 트리의 지름이라고 한다.

- 해당 문제를 해결하기 위해서는 임의의 한 점을 정한 뒤(보통 루트 노드를 선택), 해당 지점에서 가장 먼 노드를 구한다. 구한 지점을 시작지점으로 선택해서 가장 먼 노드를 구한다. 그러면 해당 길이가 트리의 지름.
    [증명 참고자료](https://koosaga.com/14)

- 예시 ([트리의 지름](https://www.acmicpc.net/problem/1167))

    ```python
    # recursion error 방지
    import sys
    sys.setrecursionlimit(10**9)

    # 정점의 개수
    V = int(input())

    # 트리 그래프
    graph = [[] for _ in range(V+1)]

    # 트리 정보
    for _ in range(V):
        tree_info = list(map(int, input().split()))
        for i in range(1, len(tree_info)-1, 2):
            graph[tree_info[0]].append([tree_info[i], tree_info[i+1]])

    # DFS
    def dfs(C, W):
        for i in graph[C]:
            a, b = i
            if distance[a] == -1:
                distance[a] = W + b
                dfs(a, W+b)

    # 시작지점 찾기
    distance = [-1] * (V+1)
    distance[1] = 0
    dfs(1, 0)
    start = distance.index(max(distance))

    # 가장 먼 곳 찾기
    distance = [-1] * (V+1)
    distance[start] = 0
    dfs(start, 0)

    # 결과 출력
    print(max(distance))
    ```