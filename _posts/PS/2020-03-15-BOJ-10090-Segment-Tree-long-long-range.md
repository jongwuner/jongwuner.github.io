---
layout:     post
title:      "BOJ 10090 - Counting Inversions"
subtitle:   "int, long long 범위에서 갯수 찾기, subsequence 구간 내에서 찾기와 비교"
date:       2020-03-15 01:49:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Segment tree
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76695571-850bfd00-66c4-11ea-9f61-f2c62b818158.png)
![image](https://user-images.githubusercontent.com/16419202/76695575-91905580-66c4-11ea-933f-d0cec7754989.png)


<br><br><br><br><br>
## Approach
- [i, i+k]내 에서 K보다 작은 갯수 찾기로 접근 했으나,
- update Query 순서고려, 현재 idx까지 update하면서, `Query(0, K-1)`를 던지면 된다. 
  - `int` 및 `long long` 전체 범위에서의 갯수를 찾으면 되는 것.


## Solution
- AC

## Comment
- 세그먼트트리의 위대함
- 응용문제 많이 풀어볼 것

## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
ll segSize = 1, N, ans;
vector<ll> seg, vl;
void update(ll idx, ll val) {
	idx += segSize;
	seg[idx] = val;
	while (idx > 1) {
		idx /= 2;
		seg[idx] = seg[2 * idx] + seg[2 * idx + 1];
	}
}
ll query(ll L, ll R, ll nodeIdx, ll nodeL, ll nodeR) {
	if (R < nodeL || nodeR < L) return 0;
	if (L <= nodeL && nodeR <= R) return seg[nodeIdx];
	ll mid = (nodeL + nodeR) / 2;
	return query(L, R, 2 * nodeIdx, nodeL, mid) + query(L, R, 2 * nodeIdx + 1, mid + 1, nodeR);
}
int main() {
	cin >> N;
	ll start = 0;
	ll end = N - 1;
	while (segSize < N) segSize = segSize << 1;
	seg.resize(segSize * 2);
	vl.resize(N);
	for (ll i = 0; i < N; i++) {
		cin >> vl[i];
	}
	for (ll i = N - 1; i >= 0; i--) {
    	ans += query(0, vl[i] - 2, 1, 0, segSize - 1);
		update(vl[i] - 1, 1);
	}
	
	cout << ans << "\n";
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/BOJ/10090.cpp)