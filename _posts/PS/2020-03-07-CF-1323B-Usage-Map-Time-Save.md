---
layout:     post
title:      "Codeforces 1323B - Count Subrectangles"
subtitle:   "'소인수분해'를 통해 key 생성, 시간복잡도 비교."
date:       2020-03-07 23:04:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Map
  - Factorization
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76159794-45469200-6167-11ea-9689-36345b38c0bf.png)
![image](https://user-images.githubusercontent.com/16419202/76159810-6ad39b80-6167-11ea-9f52-593aa4107f9c.png)


<br><br><br><br><br>
## Approach
- O(rootK*(N+M)으로 접근했다. 
- TLE <- 이거 된다. 코드오류로 인한 TLE이었음.

## Solution
- O(rootK) + O(N*rootK) + O(M*rootK)

## Comment
- Code 1번이 내풀이였는데, 이게 왜 되는거야, 시간복잡도... 

## Code 1
```cpp
#include<bits/stdc++.h>
using namespace std;
const int MAX = 40050;
int N, M, K;
long long ans;
int va[MAX], vb[MAX], cnta, cntb, sumA[MAX], sumB[MAX];
int main() {
	cin >> N >> M >> K;
	for (int i = 1; i <= N; i++) {
		cin >> va[i];
		if (va[i]) cnta++;
		sumA[i] = cnta;
	}
	for (int i = 1; i <= M; i++) {
		cin >> vb[i];
		if (vb[i]) cntb++;
		sumB[i] = cntb;
	}
 
	for (int i = 1; i * i <= K; i++) {
		if (K % i) continue;
		int div = K / i;
		int tmpA = 0, tmpB = 0;
		for (int j = 1; j + div - 1 <= M; j++) {
			if (sumB[j + div - 1] - sumB[j - 1] == div)
				tmpB++;
		}
		for (int j = 1; j + i - 1 <= N; j++) {
			if (sumA[j + i - 1] - sumA[j - 1] == i)
				tmpA++;
		}
		ans += (tmpA * tmpB);
 
		if (i == div) continue;
 
		tmpA = tmpB = 0;
		for (int j = 1; j + i - 1 <= M; j++) {
			if (sumB[j + i - 1] - sumB[j - 1] == i)
				tmpB++;
		}
		for (int j = 1; j + div - 1 <= N; j++) {
			if (sumA[j + div - 1] - sumA[j - 1] == div)
				tmpA++;
		}
		ans += (tmpA * tmpB);
	}
	cout << ans << "\n";
	return 0;
}
```

## Code 2
```cpp
#include<bits/stdc++.h>
using namespace std;
int N, M, K;
long long ans;
vector<int> via, vib, fac;
map<int, pair<int, int>> MAP;
int main() {
	cin >> N >> M >> K;
	via.resize(N + 1); vib.resize(M + 1);
	for (int i = 1; i <= N; i++) cin >> via[i];
	for (int i = 1; i <= M; i++) cin >> vib[i];
	for (int i = 1; i * i <= K; i++) {
		if (K % i) continue;
		int div = K / i;
		if (i != div) {
			fac.push_back(i);
			fac.push_back(div);
			MAP[i] = { 0, 0 };
			MAP[div] = { 0, 0 };
		}
		else {
			fac.push_back(i);
			MAP[i] = { 0, 0 };
		}
	}
 
	int cnt = 0;
	for (int i = 1; i <= N; i++) {
		if (via[i] == 1) cnt++;
		else {
			int t = 1;
			while (t <= cnt) {
				if (MAP.find(t) != MAP.end()) {
					MAP[t].first += cnt - t + 1;
				}
				t++;
			}
			cnt = 0;
		}
	}
	if (cnt != 0) {
		int t = 1;
		while (t <= cnt) {
			if (MAP.find(t) != MAP.end()) {
				MAP[t].first += cnt - t + 1;
			}
			t++;
		}
		cnt = 0;
	}
	
	for (int i = 1; i <= M; i++) {
		if (vib[i] == 1) cnt++;
		else {
			int t = 1;
			while (t <= cnt) {
				if (MAP.find(t) != MAP.end()) {
					MAP[t].second += cnt - t + 1;
				}
				t++;
			}
			cnt = 0;
		}
	}
	if (cnt != 0) {
		int t = 1;
		while (t <= cnt) {
			if (MAP.find(t) != MAP.end()) {
				MAP[t].second += cnt - t + 1;
			}
			t++;
		}
		cnt = 0;
	}
 
	for (auto now : fac) {
		ans += MAP[now].first * MAP[K / now].second;
	}
	cout << ans << "\n";
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1323B.cpp)