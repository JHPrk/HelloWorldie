# 동적 프로그래밍(Dynamic Programming)

## 동적 프로그래밍의 기본 원리
다이나믹 프로그래밍은 다음 두 가지 핵심 원칙을 기반으로 동작.
1. 분할 정복(Divide and Conquer): 문제를 더 작은, 중복되는 하위 문제로 나누기.
2. 메모이제이션(Memoization) 또는 테뷸레이션(Tabulation): 하위 문제의 결과를 저장하여 중복 계산을 방지.

### 동적 프로그래밍의 핵심 원리
- 큰 문제를 더 작은 하위 문제로 쪼개기
- 하위 문제의 결과를 메모리에 저장하여 계산 효율성 높이기
- 중복 계산을 피하고 최적의 솔루션 도출하기

## 하향식 접근법(Top-Down Approach)

- 하향식 접근법은 재귀적 방식으로 문제를 해결하고, 중간 계산 결과를 메모리에 저장하는 특징을 가짐.

### 피보나치 수열로 하향식 접근법 살펴보기

- 피보나치 수열의 정의
\[
F(n) = F(n-1) + F(n-2), \quad F(0) = 0, \quad F(1) = 1
\]
- 탑다운 방식은 재귀를 사용하여 계산한 하위 문제의 결과를 **메모리에 저장(Memoization)**하여 중복 계산을 방지.
- 이를 코드로 표현하면 다음과 같다.

```java
private Map<Integer, Integer> fibResultMap = new HashMap<>();

public int fib(int n) {
    if (fibResultMap.containsKey(n)) {
        return fibResultMap.get(n);
    }
    
    if (n <= 1) {
        return n;
    }
    
    int result = fib(n-1) + fib(n-2);
    
    fibResultMap.put(n, result);
    return result;
}
```

### 하향식 접근법의 한계를 짚어볼 것
- 재귀 호출로 인한 스택 오버플로 위험 존재
- 함수 호출 시 메모리 복제로 인한 공간적 비효율 존재

## 상향식 접근법(Bottom-Up Approach)

### 기본 상향식 피보나치 구현

```java
public int fib(int n) {
    int[] dp = new int[n+1];
    
    dp[0] = 0;
    dp[1] = 1;
    
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i-1] + dp[i-2];
    }
    
    return dp[n];
}
```

### 공간 최적화 버전으로 진화할 이유

기존 배열 기반 구현에서는 O(n) 공간을 사용했지만, 피보나치 수열의 특성상 실제로는 바로 직전 두 개의 값만 알면 됨. 따라서 다음과 같이 최적화할 수 있음:

```java
public int fib(int n) {
    int prevPrev = 0;  // n-2 번째 값
    int prev = 1;      // n-1 번째 값
    int current = 1;   // 현재 값
    
    // 3번째 항부터 n번째 항까지 계산할 것
    for (int i = 3; i <= n; i++) {
        // 새로운 current는 이전 두 값의 합
        current = prevPrev + prev;
        
        // 다음 반복을 위해 값들 시프트
        prevPrev = prev;
        prev = current;
    }
    
    return current;
}
```

### 최적화의 이점을 정리해볼 것
- 최적화를 통해 공간 복잡도를 S(1)로 줄임
- 메모리 사용량 최소화
- 시간 복잡도 O(n) 유지
- 불필요한 배열 생성 방지

## 최종 결론

동적 프로그래밍은 복잡한 문제를 효율적으로 해결하는 강력한 기법이다. 하향식과 상향식 접근법은 각자의 장단점을 가지고 있으며, 문제의 특성에 따라 적절한 방식을 선택하는 것이 핵심이다.

### 비교
**특징**            | **탑다운 (메모이제이션)**              | **바텀업 (테뷸레이션)**              |
|---------------------|--------------------------------------|-----------------------------------|
| **구현 방식**        | 재귀 기반                             | 반복문 기반                         |
| **메모리 사용량**     | 더 많음 (호출 스택 + 메모이제이션 저장) | 더 적음 (배열 또는 변수만 사용)        |
| **디버깅 용이성**     | 재귀 호출 트리로 시각화하기 쉬움         | 하위 문제 순서를 이해하기 어렵기도 함  |
| **성능**            | 시간 복잡도는 같지만 메모리 소비가 큼      | 더 공간 효율적이고 안정적  |
| **장점**            | 더 쉽게 구현 가능, 필요한 계산만 수행 가능 | 메모리 최적화 가능, 스택 오버플로가 나지 않음 |
| **단점**            | 스택 오버플로의 위험, 메모리 사용량이 많음 | 필요한 연산만 수행 불가능, 고안해내기가 어려움 |