---  
layout: single
title: "시험 감독"  
categories: Baekjoon  
tags: [c/c++, math]  
sidebar_main: true  
author_profile: true  
---  
  
## 문제: 시험 감독 (백준 13458번)  
![image](https://user-images.githubusercontent.com/68364886/156952800-7d272515-dc4e-46ef-a471-15d3fb0edfb7.png)  
![image](https://user-images.githubusercontent.com/68364886/156952842-e51b3ecb-3893-49c9-a771-03cfff779702.png)  
  
### 풀이 방법  
해당 문제는 매우 간단한 수학 및 사칙연산 문제이므로 구조분석할 필요없이 바로 풀면 된다. 우선 vector를 이용하여 각 고사실 별 인원을 입력받고 주감독관 1명을 배치 후 부감독관을 나누기와 modulo 연산을 통해서 배치하면 된다.  
  
그런데 문제를 맞게 풀었는데 틀렸다 그래서 매우 당황했다. 문제 자체가 매우 쉬워서 당연히 한번에 맞을 줄 알았는데 왜 틀렸는지 찾아봤다.  
  
결론적으로 `int` 자료형의 범위 때문에 틀렸다. int 자료형은 약 20억까지 입력받을 수 있다. 예를 들어서 주감독 관리인원 1명, 부감독 관리인원 1명,고사실 수(n의 값)가 100만, 학생 수(Ai의 값)가 100만인 경우 감독관의 수는 100만 * 100만으로 1조가 되어 정수 범위를 초과한다. 따라서 이때 오버플로우가 발생하지 않도록 하기 위해서는 `long long` 자료형을 사용해야 한다.  
  
### 코드  
```c  
#include <stdio.h>
#include <iostream>
#include <vector>
using namespace std;

long long n;
long long a, b, c;
long long cnt = 0;

int main() {
    cin >> n;
    vector<long long> V(n);
    for (long long i=0; i<n; i++) {
        cin >> a;
        V[i] = a;
    }
    cin >> b >> c;
    for (long long i=0; i<n; i++) {
        long long num = V[i];
        num -= b;
        cnt++;
        if (num <= 0) continue;
        long long subcnt = num/c;
        cnt += subcnt;
        num %= c;
        if (num != 0) cnt++; 
    }
    cout << cnt << "\n";
    return 0;
}  
```  
   
### 정리  
해당 문제는 매우 쉬운 문제였으나 수학 및 산술연산 문제의 경우 int 자료형의 범위를 초과하는지 꼭 확인해야 한다. 애매하다 싶으면 입력값에 100만이 보이는 순간 long long 자료형을 쓰면 된다.  
