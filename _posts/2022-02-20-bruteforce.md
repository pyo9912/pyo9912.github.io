---
layout: single  
title: "Brute Force"  
categories: Algorithm  
tags: [brute-force]  
toc: true  
sidebar_main: true
author_profile: true
---  

## Brute Force (브루트 포스) 란?  
Brute force란 모든 경우를 다 확인하는 방법이다. 이는 완전탐색 알고리즘으로 100% 정답을 얻을 수 있는 알고리즘이다. 이를 더 효율적으로 구현하기 위해서는 자료 탐색 시 알고리즘을 잘 설계하여 특정 구조로 탐색을 실시하는 것이다.  
- Linear search: 선형구조로 단순하게 처음부터 끝까지 탐색하는 것이다.  
- DFS: 트리구조를 가지며 깊이 우선 탐색을 실시한다.  
- BFS: 트리구조를 가지며 너비 우선 탐색을 실시한다.  
  
### 문제 풀이 방법:  
1. 주어진 문제를 구조화한다.  
2. 구조화된 문제공간에서 해를 탐색한다.  
3. 해를 구하고 정리한다.  
  
### Linear Search  
가장 간단한 예시로 1부터 10까지의 수 중 짝수의 합을 구해보자.  
```c  
int sum = 0;
for (int i=1; i<=10; i++) {
    if (i%2==0) sum += i;
}
cout << sum << "\n;
```  
이와 같이 모든 경우에 대해 순차적으로 해에 부합하는지 찾아보는 방식으로 해결하면 된다. 그러나 이와 같은 경우에는 숫자가 커지면 커질수록 시간이 오래걸린다는 치명적인 단점이 있다. 이를 해결하기 위해서 트리구조를 사용하거나 다른 방식을 이용해야 한다.  
  
### BFS  
그래프 형태의 자료구조를 탐색할 때 이용되며 트리구조를 갖는다. `BFS`의 기본 원리는 `"인접한 노드를 먼저 탐색한다."` 이다. 이는 인접한 노드를 Queue에 넣어 놓고 Queue에서 하나씩 꺼내서 탐색하는 방식으로 동작한다. 이는 아래의 특징을 갖는다.  
- Complicity(o)  
- Optimality(o)  
- Queue 사용  
- 시간복잡도: O(b^d)  
- 공간복잡도: O(b^d)  
- (b: branch 수, d: solution depth)  
    
```  
BFS 알고리즘  
1. Queue = {S}  
2. Select S  
3. is Goal(S) true?  
4. if not, Expand(S)  
```  
여기서 주의할 점은 cycle 방지를 위해서 이미 expand된 노드는 다시 Queue에 넣지 않으며, 한번 expand된 노드는 다시 expand하지 않는다.  

### DFS  
BFS와 동일한 특징을 가지며 차이점은 DFS는 Stack 자료구조를 사용한다는 점이다. `DFS`의 기본 원리는 `끝까지 탐색한다.` 이다. 이는 인접한 노드를 Stack에 넣어 놓고 Stack에서 하나씩 꺼내는 탐색하는 방식으로 동작한다. 이는 아래의 특징을 갖는다.  
- Complicity(x)  
- Optimality(x)  
- Stack 사용  
- 시간복잡도: O(b^m)  
- 공간복잡도: O(b*m)  
- (b: branch 수, m: maximal depth)
   
```  
DFS 알고리즘  
1. Stack = {S}  
2. Select S  
3. is Goal(S) true?  
4. if not, Expand(S)  
```  
마찬가지로 여기서 주의할 점은 cycle 방지를 위해서 expand된 노드는 다시 Stack에 넣지 않으며, 한번 expand된 노드는 다시 expand하지 않는다.  
  
### BFS vs DFS  
#### 시간복잡도  
- 일반적으로 BFS = DFS  
- worst case: BFS를 사용하는 것이 유리함  
- many goals, no loop, no infinite path: DFS를 사용하는 것이 유리함  
    
#### 공간복잡도  
- DFS가 linear한 space를 가지므로 유리함  
    
#### 정리  
- BFS는 goal이 근처에 있을떄 유리함  
- DFS는 메모리 관점에서 유리함  

