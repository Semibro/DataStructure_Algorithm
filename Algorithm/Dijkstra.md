# 다익스크라 (Dijkstra)

- 개념

  1. 그래프에서 한 정점(노드)에서 다른 정점까지 최단 경로를 구하는 알고리즘

  2. 도착 정점 뿐만 아니라 모든 다른 정점까지 최단 경로를 방문하며 각 정점까지의 최단 거리를 탐색

- 벨만-포드 알고리즘과 차이점

  [해당 내용 참고](https://github.com/Semibro/DataStructure_Algorithm/blob/main/Algorithm/Bellman-Ford.md)

- 수행과정

  1. 출발 노드와 도착 노드를 설정

  2. '최단 거리 배열'을 초기화 (임의의 큰수로 설정)

  3. 현재 위치한 노드의 인접 노드 중 방문하지 않은 노드를 구별 후, 방문하지 않은 노드 중 거리가 가장 짧은 노드를 선택. 그 노드를 방문 처리

  4. 해당 노드를 거쳐 다른 노드로 넘어가는 비용을 계산하여 '최단 거리 배열'을 업데이트

  5. 3~4 과정을 반복

- 예시

  1. [택배 배송](https://www.acmicpc.net/problem/5972)

  [풀이]

  ```Python
  from heapq import heappush, heappop

  # INPUT
  N, M = map(int, input().split())
  Farm = [[] for _ in range(N+1)]

  # INPUT (무방향 그래프 생성)
  for _ in range(M):
      A, B, C = map(int, input().split())
      Farm[A].append((B, C))
      Farm[B].append((A, C))

  # INF값을 초기값으로 설정한 배열 생성
  distance = [9876543210] * (N+1)

  # heapq 사용을 위한 배열 생성
  heap = []
  distance[1] = 0  # 시작위치는 0
  heappush(heap, (0, 1))  # 시작위치는 heapq에 넣는다.

  # heap이 끝날 때까지 그래프를 확인하면서 최단거리 파악
  while heap:
      dist, current = heappop(heap)
      if distance[current] >= dist:
          for next in Farm[current]:
              temp_dist = dist + next[1]
              if temp_dist < distance[next[0]]:
                  distance[next[0]] = temp_dist
                  heappush(heap, (temp_dist, next[0]))

  print(distance[N])
  ```