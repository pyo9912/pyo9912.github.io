---
layout: "single"
title: "회의실 배정"
categories: Baekjoon
tags: [c/c++, greedy, vector, sort]
sidebar_main: true
author_profile: true
---  

## 문제: 회의실 배정 (백준 1931번)  
![image](https://user-images.githubusercontent.com/68364886/154469752-a0c902b7-c98d-4624-8017-19215f2be7d0.png)  
  
### 구조 분석  
전형적인 Greedy algoritm 문제이다. 해당 문제의 풀이 방법은 각 회의를 먼저 끝나는 순서대로 나열을 한 뒤 앞에서부터 고르면 되는 것이다. 알고리즘 자체는 매우 간단하며 쉽게 풀리도록 연습해야 한다.  
  
### 코드  
```c  
#include <stdio.h>
#include <stdlib.h>
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

typedef struct Time {
    int start;
    int end;
} Time;

bool compare(Time t1, Time t2) {
    if (t1.end == t2.end) {
        // 회의의 끝나는 시간이 같다면
        // 먼저 시작하는 회의가 앞에 오도록 한다.
        return t1.start < t2.start;
    }
    else {
        // 각 회의를 먼저 끝나는 순서대로 나열한다.
        return t1.end < t2.end;
    }
}

int main() {
    int N;
    cin >> N;
    vector<Time> V(N);
    for (int i=0; i<N; i++) {
        cin >> V[i].start >> V[i].end;
    }

    sort(V.begin(),V.end(),compare);

    int cnt = 0;
    int time = 0;
    for (int i=0; i<V.size(); i++) {
        if (time <= V[i].start) {
            time = V[i].end;
            cnt++;
        }
    }

    cout << cnt << "\n";
    return 0;
}
```  
  
### 풀이 방법  
해당 문제를 풀 때 정렬하는 작업이 필요하다. 이를 위해서는 `STL vector`와 `sort()`를 이용하면 쉽게 할 수 있다. 우선 `sort()`를 하기 위해서는 `<algorithm>`헤더를 추가해야한다.  
  
`STL vector`를 이용해서 sort를 실시하기 위해서는 비교를 위한 compare함수를 만들어야 한다.  
```c  
bool compare(Time t1, Time t2) {
    if (t1.end == t2.end) {
        return t1.start < t2.start;
    }
    else {
        return t1.end < t2.end;
    }
}  
```  
해당 부분이 이에 해당하며 이를 sort()의 세번째 parameter에 추가해준다.  
```c  
sort(V.begin(),V.end(),compare)  
```  
이를 통해서 vector의 시작부터 vector의 끝부분까지 compare에서 작성한 기준으로 정렬을 할 수 있다.  
  
### 정리  
해당 문제는 기본적인 greedy algorithm을 구현하는 문제였다. 이런 문제는 크게 어렵지 않으므로 익숙해지도록 연습해야한다.  
