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
