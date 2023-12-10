# 피보나치 (피사노 주기)

- 피보나치를 푸는 방법에는 다양한 것이 있지만, 굉장히 큰 수를 10의 배수로 나누는 문제는 피사노 주기를 사용

- 피사노 주기 : 피보나치 수를 K로 나눈다고 할 때, 그 나머지는 항상 주기를 가지게 됨

    ```
    피사노 주기를 P라고 했을 때,

    N % M = (N % P) % M

    특히, M = 10^k이고 k>2일 때,

    15 * 10^(k-1)이 성립
    ```

- 예시 ([피보나치 수 3](https://www.acmicpc.net/problem/2749))

    ```python
    n = int(input())
    fibo = [0, 1]
    mod = 1000000
    # 피사노 주기를 활용하여 계산
    # 피사노 주기에 따라 나누는 값(M = 10^k(k>2))의 -1승을 15에 곱한다.
    # 15 * 10^(k-1)
    pisano = 15 * (mod // 10)

    if n == 0:
        print(fibo[0])
    elif n == 1:
        print(fibo[1])
    else:
        for i in range(2, pisano):
            fibo.append(fibo[i-1] + fibo[i-2])
            fibo[i] = fibo[i] % mod
        print(fibo[n%pisano])
    ```