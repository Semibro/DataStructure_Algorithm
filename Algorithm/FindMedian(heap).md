# 중간값 구하기 (Find Median)

- 힙(heap)/우선순위 큐(priority queue)를 사용하여 중간값을 빠르게 구하는 알고리즘

- 예시 ([가운데를 말해요](https://www.acmicpc.net/problem/1655))

    ```python
    import heapq

    max_heap = [] # 최대 힙
    min_heap = [] # 최소 힙

    def findMid(num):
        # push
        if len(max_heap) == len(min_heap):
            heapq.heappush(max_heap, -num)
        else:
            heapq.heappush(min_heap, num)

        # swap
        if len(max_heap) != 0 and len(min_heap) != 0 and -max_heap[0] > min_heap[0]:
            temp_max = heapq.heappop(max_heap)
            temp_min = heapq.heappop(min_heap)

            heapq.heappush(max_heap, -temp_min)
            heapq.heappush(min_heap, -temp_max)

        # print
        return -max_heap[0]
    ```

    ```
    [ 해설 ]

    두 개의 heap을 사용해서 풀이 가능

    한 쪽의 heap은 max_heap으로 최댓값이 힙의 처음에 나오도록 만들고, 다른 heap은 min_heap으로 최솟값이 힙의 처음에 나오도록 만든다.

    만약 max_heap과 min_heap의 길이가 값다면 max_heap에 넣고, 아니라면 길이를 맞추기 위해 min_heap에 넣어준다.

    여기서 핵심!
    max_heap의 첫 번째 값이 min_heap의 값보다 크다면 둘의 위치를 swap 해준다. 이를 통해 중앙값을 맞춰간다.
    ```