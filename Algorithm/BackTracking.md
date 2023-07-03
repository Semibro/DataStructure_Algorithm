# 백트래킹 (BackTracking)

- 백트래킹은 해를 찾는 도중 결과와 상관없는 부분을 만나면 되돌아가서 다시 해를 찾아가는 방법

- 백트래킹은 최적화(Optimization)문제와 결정(Decision)문제를 해결할 때 유용

- 예시

    1. [N-Queen](https://www.acmicpc.net/problem/9663)

    [풀이]

    ```Python
    import sys
    input = sys.stdin.readline

    N = int(input())
    answer = 0
    col_visited = [0] * N  # 열 체크를 위한 리스트
    right_up_visited = [0] * (2*N)  #오른쪽 위로 올라가는 대각선 체크를 위한 리스트
    left_up_visited = [0] * (2*N)  #왼쪽 위로 올라가는 대각선 체크를 위한 리스트

    def dfs(n):
        global answer
        if n == N:  # N행까지 갔다면 종료 (성공했다는 의미)
            answer += 1
            return
        for y in range(N):
            if col_visited[y] == right_up_visited[n+y] == left_up_visited[n-y] == 0:
                col_visited[y] = right_up_visited[n+y] = left_up_visited[n-y] = 1
                dfs(n+1)
                col_visited[y] = right_up_visited[n+y] = left_up_visited[n-y] = 0
                
    dfs(0)
    print(answer)
    ```

- 백트래킹과 깊이우선탐색의 차이

    1. 어떤 노드에서 출발하는 경로가 해결책으로 이어질 것 같지 않다면 더 이상 경로를 탐색하지 않음으로써 시도의 횟수를 줄임 (가지치기, Prunning)

    2. 깊이우선탐색이 모든 경로를 추적하는것과 다르게 백트래킹은 불필요한 경로를 사전에 차단

    3. 깊이우선탐색을 가하기에 경우의 수가 많은 경우 즉 N!가지의 경우의 수를 가진 문제에 대해 깊이우선탐색을 진행하면 시간복잡도가 상승

    4. 백트래킹 알고리즘을 적용하면 일반적으로 경우의 수가 줄어들지만 이 역시 최악의 경우 Optimal한 solution은 아님