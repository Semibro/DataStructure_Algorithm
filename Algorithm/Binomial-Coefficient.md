# 이항계수 (Bionomial Coefficient)

- 조합론에서 이항 계수는 이항식을 이항 정리로 전개했을 때 각 항의 계수이며, 주어진 크기의 조합의 가짓 수

    <img src='https://github.com/Semibro/Baekjoon/assets/71372469/d47aec22-fa60-4b79-95b9-65787c0914d1'>

- 예시 ([이항 계수3](https://www.acmicpc.net/problem/11401))

    ```python
    N, K = map(int, input().split())
    MOD = 1000000007

    def binomial_coefficient(n, k):
        fact = [1] * (n+1)

        # 팩토리얼
        for i in range(1, n+1):
            fact[i] = (fact[i-1] * i) % MOD

        # 모듈러 연산을 사용한 역원 계산
        def mod_inverse(x):
            return pow(x, MOD-2, MOD)

        num = fact[n]
        denominator = (fact[k] * fact[n-k]) % MOD

        return (num * mod_inverse(denominator)) % MOD

    print(binomial_coefficient(N, K))
    ```

    ```
    해당 문제에서 시간복잡도를 줄이기 위해 모듈러 연산을 사용해 시간복잡도를 최소화

    이항계수 C(n,k)를 구하는 과정에서 팩토리얼 값을 직접 계산하는 대신, 모듈러 연산을 사용하여 역원을 활용
    ```

    ```
    모듈러 연산에서 역원은 a에 대해서 a^-1로 표시

    a*a^-1 ≡ 1 (mod p)이 성립 (여기서 p는 모듈러 연산에 사용되는 소수)
    ```

    ```
    페르마의 소정리와 모듈러 역원을 이용하여 이항계수 구하기

    1. 팩토리얼 값 대신 모듈러 역원을 사용하여 n!, k!, (n-k)!의 값 구하기

    2. 페르마의 소정리에 따라 a^(p-1) ≡ 1 (mod p)이 성립하는 것을 활용해 a^(p-2) 계산

    3. 이를 이용해 이항계수 계산

    해당 과정을 통해 이론상으로 O(logn)
    ```