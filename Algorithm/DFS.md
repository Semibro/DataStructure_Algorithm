# 깊이우선탐색 (DFS)

- 비선형구조의 그래프에서는 그래프로 표현된 모든 자료를 탐색하는 것이 중요!

- 그래프의 모든 자료를 깊이 우선으로 탐색하는 방법이 있음

- 시작 정점의 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이우선으로 탐색을 진행하여 더 이상 탐색할 곳이 없다면 되돌아와서 다른 방향의 정점을 탐색하여 모든 정점을 탐색하는 방법

- 깊이우선탐색 알고리즘 개념

    1. 시작 정점v를 결정하여 방문
    2. 정점 v에 인접한 정점 중

        a. 방문하지 않은 정점 w가 있다면, 정점 v를 스택에 push 후, 정점 w를 방문 그리고 정점 w를 v로 바꾸고 다시 진행

        b. 방문하지 않은 정점이 더 이상 없다면, 스택의 pop을 통해 가장 마지막 방문 정점을 v로 설정하여 다시 진행

    3. 스택이 공백이 될 때까지 반복


- 인접행렬 / 인접리스트
  
    1. 인접행렬

    ```python
    # ver1 (인접행렬)
    V, E = map(int, input().split())
    arr = list(map(int, input().split()))
    adjM = [[0]*(V+1) for _ in range(V+1)]
    for i in range(E):
		v1, v2 = arr[i*2], arr[i*2+1]  # 2개씩 불러옴
		adjM[v1][v2] = 1
		adjM[v2][v1] = 1
    ```

    2. 인접리스트

    ```python
    # ver2 (인접리스트)
    V, E = map(int, input().split())
    arr = list(map(int, input().split()))
    adjL = [[] for _ in range(V+1)]
    for i in range(E):
		v1, v2 = arr[i*2], arr[i*2+1]  # 2개씩 불러옴
		adjL[v1].append(v2)
    ```

- 깊이우선탐색

    ```python:DFS.py
    graph = [[0] * 8 for _ in range(8)]  # 그래프를 만들어서 시작

    n = int(input())  # 입력부분
    for _ in range(n):  # for문입력부분
        a, b = map(int, input().split())
        # 인접행렬사용 / 인접리스트 사용 시 위와 코드 참조
        graph[a][b] = 1  # 무방향 그래프의 경우 양쪽으로 다 받아준다.
        graph[b][a] = 1

    visited = [False] * 8  # 방문여부 처리를 위한 visited배열 생성
    stack = []  # 스택 생성
    res = []  # 결과 저장 리스트 생성

    v = 1  # 시작점이 1일경우
    visited[v] = True  # 방문처리
    res.append(v)  # 결과에 추가

    while True:  # while문을 사용하여 stack이 전부 빠질때까지 작동
        for w in range(8):
            if graph[v][w] and not visited[w]:  #그래프를 이용해 움직이면서 방문하지 않은 곳
                stack.append(v)  # 스택에 추가
                v = w  # w를 v로 변경
                visited[w] = True # w 방문함
                res.append(w)  # 결과에 추가
                break
        else:
            if stack:  # stack에 추가할 것이 없다면
                v = stack.pop()  # pop을 통해서 v값 다시 설정
            else: # 스택이 비어있으면
                break
    print('-'.join(map(str, res)))
    ```