---
layout:     post
title:      "Codeforces 1316A - Grade Allocation"
subtitle:   "오직 결과값을 구하기위해 단순하게 생각하자"
date:       2020-03-07 14:02
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - find real problem
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76137118-86ae4300-607c-11ea-9eac-2276b89faeec.png)

<br><br><br><br><br>
## Approach
- 결국 첫번째 요소에다가 maxium으로 모두 옮겨주면 되는 문제.
- 입력받으면서, 모든 값을 다 더해주면 되는 문제인데, 문제조건을 그냥 꽈서 줬을 뿐이다.

## Solution
- Approach와 동일

## Comment
- 이런 A번 유형이 상당히 많다. 정말 물어보고 싶은게 무엇인지.
- 문제조건을 놓치면 상당히 해맬수 있다.

## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
vector<ll> vl;
ll N, M, sum, tsum;
int main() {
	int T; cin >> T; while (T--) {
		sum = tsum = 0;
		vl.clear();
 
		cin >> N >> M;
		vl.resize(N + 1);
		for (ll i = 1; i <= N; i++) {
			cin >> vl[i];
			if(i > 1) tsum += vl[i];
		}
		if (vl[1] + tsum >= M) cout << M << "\n";
		else cout << vl[1] + tsum << "\n";
	}
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1316A.cpp)