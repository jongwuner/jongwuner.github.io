---
layout:     post
title:      "Codeforces Ozon Tech Challenge 1305A - Kuroni and the Gifts"
subtitle:   "Ai, Bi 값이 다를때, 정렬을 해서 얻는 결과"
date:       2020-03-04 04:23:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Sort
  - Distinct Value
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/75812166-18922380-5dd1-11ea-9fee-b8a7e5cb2b7d.png)

<br><br><br><br><br>
## Approach
- 완전탐색 
  - N*N? N*N*N ? 백트래킹?
 
## Solution
- `Sort` -> Greedy
- a와 b가 완전 똑같다 하더라도,  a + b의 순서는 보장된다.

## Comment
- 다른값으로 주어질 때, 정렬하는 것. 
- `문제의 조건, ai, bi는 모두 다른값으로 주어진다.`라는 조건을 분명히 읽었어야 한다.
- 문제의 조건을 놓치면 대회를 놓치는 경우가 있다. 


## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
int N;
vector<ll> v1, v2;
int main() {
	int T; cin >> T; while (T--) {
		v1.clear(); v2.clear();
		cin >> N;
		v1.resize(N); v2.resize(N);
		for (int i = 0; i < N; i++) cin >> v1[i];
		for (int i = 0; i < N; i++) cin >> v2[i];
		sort(v1.begin(), v1.end());
		sort(v2.begin(), v2.end());
		for (int i = 0; i < N; i++) 
			cout << v1[i] << " ";
		cout << "\n";
		for (int i = 0; i < N; i++)
			cout << v2[i] << " ";
		cout << "\n";
 
	}
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1305A.cpp)
