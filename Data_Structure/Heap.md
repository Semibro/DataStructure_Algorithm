# 힙 (Heap)

- 힙(heap) 이란?
  
    1. 최댓값 및 최솟값을 찾아내는 연산을 빠르게 하기 위해 고안된 완전이진트리(Complete binary tree)를 기본으로 한 자료구조

    ```
    A가 B의 부모노드이면 A의 key 값과 B의 key 값 사이에는 대소관계가 성립
    ```

- 힙의 종류

    1. 최소 힙(min heap) : 부모노드의 키 값이 자식노드의 키 값보다 항상 작은 힙

    2. 최대 힙(max heap) : 부모노드의 키 값이 자식노드의 키 값보다 항상 큰 힙

- 힙 사용하기

    1. 파이썬에서는 알고리즘을 제공

        ```python
        import heapq
        ```

    2. 생성하기

        ```
        heappush(heap, item) : 빈 리스트(heap)를 만들어서 원소(item)을 추가

        heapify(list) : 리스트를 힙으로 변경
        ```

        [ 예시 ]

        ```python
        heap = []

        heapq.heappush(heap, 5)
        heapq.heappush(heap, 8)
        heapq.heappush(heap, 2)

        print(heap) # ans : [2, 5, 8]
        ```

        ```python
        lst = [8, 3, 5]
        heapq.heapify(lst)

        print(lst) # ans : [3, 5, 8]
        ```

    3. 삭제하기

        ```
        heappop(heap) : 힙에서 가장 작은 원소를 제거
        ```

        ```python
        heap = [1, 6, 38, 57]

        print(heapq.heappop(heap)) # ans : 1
        print(heap) # ans : [6, 38, 57]
        ```

    4. 최대 힙 (응용)

        ```python
        # heapq는 최소 힙만 가능하므로 응용이 필요

        import heapq

        nums = [8, 4, 3, 9, 5, 7]
        tuple_heap = []
        max_heap = []

        for num in nums:
            heapq.heappush(tuple_heap, (-num, num)) # (우선순위, 값)
        
        print(tuple_heap)
        # [(-9, 9), (-8, 8), (-7, 7), (-5, 5), (-4, 4), (-3, 3)]

        for i in range(len(tuple_heap)):
            temp = heapq.heappop(tuple_heap)[1]
            max_heap.append(temp)

        print(max_heap)
        # [9, 8, 7, 5, 4, 3]
        ```