---
layout:     post
title:      "Codeforces 1316B - Grade Allocation"
subtitle:   "String 연산자, 규칙은 뇌비우고 뜯어봐야 한다, 단순한 규칙앞에서 멍때리지 말자, 홀짝규칙 기준"
date:       2020-03-07 14:04:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - String
  - Find Pattern(Simple)
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76137127-9a59a980-607c-11ea-95cb-ef535ada56ec.png)
![image](https://user-images.githubusercontent.com/16419202/76137132-a7769880-607c-11ea-93c9-f8c46a490d16.png)

<br><br><br><br><br>
## Approach
- 규칙을 찾으러 들어가기까지 결단이 안선다. 
- 규칙을 찾다가 홀짝규칙에서 또 시간 많이 사용.

## Solution
- 단순한 규칙 + 홀짝규칙 만 찾으면, 시간소비할 문제가 아니었다.

## Comment
- Q. 단순한 규칙에 오래 시간을 쏟는 이유가 뭐였을까?

## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
vector<ll> vl;
map<ll, ll> Map1;
ll N, M;
bool ans = true;
int main() {
	cin >> N >> M;
	vl.resize(N);
	for (ll i = 0; i < N; i++) {
		cin >> vl[i];
		if (Map1.find(vl[i]) != Map1.end()) {
			ans = false;
		}
		else Map1[vl[i]] = 1;
	}
	if (N >= M + 10) ans = false;
	ll res = 1;
	if (ans) {
		for (ll i = 0; i < N; i++) {
			for (ll j = i + 1; j < N; j++) {
				res *= abs(vl[i] - vl[j]);
				res %= M;
				if (res == 0) {
					ans = false;
					break;
				}
			}
			if (!ans) break;
		}
	}
 
	if (!ans) {
		cout << "0\n";
	}
	else cout << res << "\n";
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1305C.cpp)
- [Modulus 활용 -(1)](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1295D.cpp)
- [Pigeon Hall 활용 - (1)]()