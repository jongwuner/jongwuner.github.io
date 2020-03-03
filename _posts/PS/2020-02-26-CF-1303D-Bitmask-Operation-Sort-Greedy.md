---
layout:     post
title:      "Codeforces Round 82 1303D - Fill The Bag"
subtitle:   "비트마스크의 연산이 자유자재로 되는가?, 비트마스크 그리디, 비트마스크스럽게 정렬"
date:       2020-02-26 14:04:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Construction
  - Bitmask
  - Sort
  - Greedy
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/75780030-0ea2fd00-5d9e-11ea-864d-dec6d1d90eac.png)
<br><br><br><br><br>
## Approach
- 입력이 2^n의 꼴이기 때문에, 무조건 같은 수 두개를 더하면, `Shift Left`의 효과를 얻게 된다. 
- 

## Solution
- `Pair<Int, String>` 사용해서 모든 값을 넣어두고
- Pop하면서 수정하고, 
- Pop했다가 수정한 것 다시 Push하고, 
- 결과출력의 과정.


## Comment
- `실수한 부분` : 테스트케이스에 의존하여 다른 경우를 보지못함. 합을 만들어야 하는 기준이 되는 숫자보다 큰 값이 들어왔을 때, 
  - 교착상태로 어마어마한 시간을 허비했다. 
  - 모든경우를 살피지 못하고, 알고리즘을 결국 다시 짜야했다. 

## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
int M;
ll N, ans;
vector<ll> vl;
int main() {
	ios_base::sync_with_stdio(false);
	cin.tie(0); cout.tie(0);

	int T; cin >> T; while (T--) {
		// clear
		ans = 0;
		vl.clear();
		// init
		int tmp;
		cin >> N >> M;
		for (int i = 0; i < M; i++) cin >> tmp, vl.push_back(tmp);

		sort(vl.begin(), vl.end());

		ll nptr = 1;
		ll sum = 0;
		int idx = 0;
		while (idx < M && N) {
			while ((N & nptr) != nptr) 
				nptr = nptr << 1;

			while (idx < M && sum < nptr) 
				sum += vl[idx], idx++;

			if (idx >= M && sum < nptr) break;

			ll nlsb = 1, slsb = 1;
			while (N >= nlsb) nlsb = nlsb << 1; nlsb = nlsb >> 1;
			while (sum >= slsb) slsb = slsb << 1; slsb = slsb >> 1;


			ll cnt = 0;
			if (slsb == nptr) {
				sum = sum >> cnt;
				sum -= nptr;
				N = (N | slsb) - slsb;
				ans += cnt;
			}
			else {
				while ((slsb & nptr) != nptr) {
					cnt++;
					slsb = slsb >> 1;
					N = (N | slsb) - slsb;
				}
				sum = sum >> cnt;
				sum -= nptr;
				N = (N | slsb) - slsb;
				ans += cnt;
			}
		}
		if (N) ans = -1;
		cout << ans << "\n";
	}
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1303D.cpp)