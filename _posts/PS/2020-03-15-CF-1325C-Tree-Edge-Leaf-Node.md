---
layout:     post
title:      "Codeforces 1325C - Ehab and Path-etic MEXs"
subtitle:   "TREE의 리프노드를 찾아서, Greedy로, TREE내부의 모든경로의 기준은 LEAF노드이니까?"
date:       2020-03-15 01:49:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Graph
  - Tree
  - Greedy
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76695508-c7810a00-66c3-11ea-885a-88b9f24c3136.png)
![image](https://user-images.githubusercontent.com/16419202/76695514-d2d43580-66c3-11ea-844e-64ff91108a18.png)



<br><br><br><br><br>
## Approach
- 인접 노드의 수로 판단을 하는건지?
- 리프노드부터 해결을 하는건지?

## Solution
- 리프노드에서는 가장 작은 숫자부터
- 리프노드가 아니면 가장 큰 숫자부터 넘버링한다.

## Comment
- 내가 생각한 증명.
  - 정점이 N개인 트리내부 임의의 경로 (u, v)는 리프노드를 최대 2개 포함하게 되는데, (u, v)에서 리프노드가 아닌 노드는, [N - M, N - 1]의 번호를 가지고 있다. 리프노드는 [0, M - 1]의 번호를 가지고 있으므로, 경로의 길이가 N이 아니라면, min(0, 1, 2)값을 항상 가진다?
- 트리 경로 성질
- 트리에서 임의의 경로 [u, v]는 유일하다.

## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
const int MAX = 1e5 + 10;
int N, cnt, Rcnt;
int ea[MAX], eb[MAX], num[MAX];
vector<vector<int>> adj;
int main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
 
	cin >> N;
	adj.resize(N + 1); 
	for (int i = 1; i <= N - 1; i++) {
		int a, b;
		cin >> a >> b;
		a--; b--;
		ea[i] = a;
		eb[i] = b;
		adj[a].push_back(b);
		adj[b].push_back(a);
	}
 
	Rcnt = N - 2;
	for (int i = 1; i <= N - 1; i++) {
		int A = ea[i];
		int B = eb[i];
		if (adj[A].size() == 1 || adj[B].size() == 1) {
			cout << cnt++ << "\n";
		}
		else {
			cout << Rcnt-- << "\n";
		}
	}
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1325C.cpp)