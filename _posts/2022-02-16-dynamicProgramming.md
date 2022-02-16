---
layout: single  
title: "Dynamic Programming"  
categories: Algorithm  
tags: [dynamic-programming]  
toc: true  
sidebar_main: true
author_profile: true
---  

## Dynamic Programming (동적 계획법) 이란?  
주어진 `problem`을 작은 `subproblem`으로 나눠 푼 다음 이를 통해 최종 답을 얻는 방식  
이를 충족하기 위해서는 다음의 조건이 필요하다.  
1. 주어진 `problem`을 작은 규모의 `subproblem`으로 나눌 수 있는가?  
2. `subproblem`으로부터 얻은 `solution`으로 상위 `problem`의 답을 얻을 수 있는가?  
3. `subproblem`이 중복되어 사용되는가? 즉, `memoization`이 적용가능한가?  
  
이 조건을 충족하는 경우 dynamic problem을 이용하여 문제를 풀 수 있다.  
  
## Without Dynamic Programming  
Dynamic programming이 적용되지 않는 예제를 먼저 확인해보자. 에를 들어 n번째 피보나치 수를 구하는 fib 함수를 만들면 다음과 같이 코드를 작성할 수 있다.  
```c  
int fib(int n) {
    if (n==0) return 0;
    else if (n==1) return 1;
    else {
        return fib(n-1) + fib(n-2);
    }
}
```
  
이와 같은 방벙으로 recursion을 이용하여 n번째 피보나치 수를 구하는 함수를 만들 수 있다. 예를 들어 5번째 피보나치 수를 구하는 경우 아래의 그림과 같이 함수가 호출될 것이다.  
![image](https://user-images.githubusercontent.com/68364886/154256186-ac6c03c5-ef0a-43ca-9492-647ed09d0334.png)  
이 경우 O(2^N)의 시간복잡도를 갖는다. 해당 함수의 실행 시간을 더 줄이기 위해 우리는 반복적으로 사용되는 fib(3)이나 fib(2)의 결과 값을 따로 저장하는 memoization 기법을 이용할 수 있다. 이를 통해 fib(3)이나 fib(2)를 여러번 호출하지 않고 구하고자 하는 답을 얻을 수 있다.  

## Top-down 방식  
Dynamic programming을 실시할 때 쉽게 떠올릴 수 있는 직관적인 방식이다. 이는 이전과 같이 `recursion`을 이용하여 설계할 수 있다. 이는 `memoization`을 이요하기 위한 배열을 생성하여 해당 배열에 fib()함수의 결과 값을 저장한다. 이후 fib()함수가 호출 될 때 결과값이 배열에 있다면 굳이 계산을 또 하지 않고 결과값을 바로 이용한다.  
```c
int memo[MAX] = {0,};  
  
int fib(int n) {
    if (memo[n] != 0) return memo[n];
    if (n == 1 || n == 2) memo[n] = 1;
    else {
        memo[n] = fib(n-1) + fib(n-2);
    }
    return memo[n];
}
```  
이와 같은 방식으로 n번째 피보나치 수를 구하는 경우 아래의 그림과 같이 중복되는 subproblem에 대해 계산을 실시하지 않고 답을 구할 수 있다.  
![image](https://user-images.githubusercontent.com/68364886/154256273-9ac032fb-92ff-44e4-9de7-92c635b226df.png)  
이 경우 O(N)의 시간복잡도와 O(N)의 공간복잡도를 갖는다. 왜냐하면 fib(1)을 구한 값이 fib(2)에 이용되고, fib(2)를 구한 값이 fib(3)에 이용되는 것으로 최종 답까지 이어지기 때문이다. 공간복잡도의 경우 fib(n)을 구하기 위해서 크기 n의 배열만 있으면 되므로 O(N)이 된다.  
그러나 이와 같이 `top down`방식은 `recursive`하게 호출된다는 단점이 있다. n번째 피보나치 수를 구하려 할 때, recursive한 구조에 따라 함수를 실행하기 위해서 stack frame을 계속하여 호출하게 되며 n값이 매우 큰 경우에는 stack overflow가 발생하게 된다. 이떄 `bottom up` 방식을 이용하게 되면 해당 문제를 해결할 수 있다.  
  
## Bottom-up 방식  
이는 `recursion`이 아닌 `반복문`을 이용하는 방식이다. 이전의 `top down ` 방식에서는 fib(n)을 구하기 위해 fib(n-1)과 fib(n-2)를 구하는 순서로 진행을 했다면 `bottom up` 방식에서는 fib(0)부터 하나씩 배열의 값을 채우는 순서로 진행한다. 이를 코드로 작성하면 다음과 같다.  
```c  
int memo[MAX] = {0,};

int fib(n) {
    memo[0] = 0;
    memo[1] = 1;
    for (int i=2; i<=n; i++) {
        memo[i] = memo[i-1] + memo[i-2];
    }
    return memo[n];
}
```  
이 경우 마찬가지로 O(N)의 시간복잡도와 O(N)의 공간복잡도를 갖는다. 그러나 반복문을 이용하는 경우, 재귀함수를 이용할 때의 오버헤드를 줄일 수 있어서 성능이 더 좋아진다. `bottom up` 방식에서 사용되는 결과값 저장용 배열은 `DP table`이라고 한다.  
