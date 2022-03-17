---  
layout: single
title: "스타트와 링크"  
categories: Baekjoon  
tags: [c/c++, back-tracking, dfs]  
sidebar_main: true  
author_profile: true  
---  


## 문제: 스타트와 링크 (백준 14889번)  
![image](https://user-images.githubusercontent.com/68364886/158729113-51786a04-e0f8-4b06-8eae-42e3dbc5bd75.png)  
![image](https://user-images.githubusercontent.com/68364886/158729246-3d0764b8-ee55-46e2-abb3-5c239d264047.png)  
![image](https://user-images.githubusercontent.com/68364886/158729284-e51bebef-7eb0-4154-a135-533f314af8f4.png)  
  
### 구조 분석  
해당 문제의 경우 처음에 배열 또는 벡터로 문제를 풀어야 하는지 고민했다. 백터로 능력치를 저장하고 이를 sort하고 다시 나누는 것은 그러나 항상 optimal한 값을 출력할 것 같지 않았다. 그래서 고민하다가 힌트를 보니 브루트포스 백트래킹 문제였다.  
  
처음에는 이게 왜 백트래킹이지? 하고 생각했는데 조금 더 생각해보니 팀을 나누는 모든 경우를 고려하여 팀 격차의 최소값을 산출하는 작업을 통해서 문제를 풀 수 있다고 생각했다.  
  
### 풀이 방법  
각 level에서 start와 link의 값을 더하기보다는 방문하면서 팀을 표기하기 위한 일차원 배열을 하나 선언하고 해당 배열에 0 또는 1로 팀을 표시하도록 한다. 그리고 level이 n/2가 되는 순간 팀 분할이 끝나므로 해당 시점에서 start와 link의 능력치를 각각 더하고 두 능력치 합의 차이를 산출하도록 한다. 이전까지의 dfs 백트래킹 문제에서는 각 level에서 계산을 실시했는데 이 문제에서는 다음 recursion 호출을 편하게 하기 위해서 계산을 마지막으로 미뤄줬다.  
  
### 코드  
```c
#include <stdio.h>
#include <iostream>
#include <math.h>
using namespace std;

int n;
int start, link;
int ans = 1000000000;
int S[20][20];
int visited[20];

void dfs(int level, int pos) {
    if (level == n/2) {
        start = 0;
        link = 0;
        for (int i=0; i<n; i++) {
            for (int j=0; j<n; j++) {
                if (visited[i] == 0 && visited[j] == 0) start += S[i][j];
                if (visited[i] == 1 && visited[j] == 1) link += S[i][j];
            }
        }
        ans = min(ans, abs(start-link));
    }
    for (int i=pos; i<n; i++) {
        visited[i] = 1;
        dfs(level + 1, i + 1);
        visited[i] = 0;
    }
}

int main() {
    cin >> n;
    for (int i=0; i<n; i++) {
        for (int j=0; j<n; j++) {
            cin >> S[i][j];
        }
    }
    dfs(0,0);
    cout << ans << "\n";
    return 0;
}  
```  
  
### 정리  
기본적인 dfs 백트래킹 문제였으나 해당 문제 카테고리를 바로 알아차리지 못해서 아쉽고, 또 풀이 방법에 기술했듯이 각 level에서 계산하기 보다는 마지막에 몰아서 계산하는 방법이 편하다는 것을 고려해야했다. 그리고 무엇보다 중요한 ans값 초기화!! 최댓값, 최솟값을 산출하는 문제에서는 초기화가 필수이다.  

