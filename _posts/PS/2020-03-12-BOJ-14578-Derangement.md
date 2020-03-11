---
layout:     post
title:      "BOJ 14578 - 영훈이의 색칠공부"
subtitle:   "교란순열, 행-사람, 열-모자"
date:       2020-03-12 00:47:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Derangement
  - find real problem
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76434716-61616200-63f9-11ea-89e4-6000aa73c869.png)
![image](https://user-images.githubusercontent.com/16419202/76434743-6cb48d80-63f9-11ea-8477-594f0096f1e9.png)


<br><br><br><br><br>
## Approach
- 왼쪽 상단에 두고, 오른쪽 아래에다가 두면, i-2의 꼴이 나온다. 

## Solution
- 조금 더 전형적인 문제였다. (교란순열 * N!) 
- 모자 및 사람에 대해서 번호를 N*!으로 부여한다.

## Comment
- 행과 열을 모자와 사람으로 바라볼 수 있었는지, `find real problem`

## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int MAX = 1e5 + 50;
ll MOD = 1000000007;
ll facto[MAX] = { 1, 1, 2 };
ll N, dp[MAX] = { 0, 0, 1 };
int main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);

	cin >> N;
	for (int i = 3; i <= N; i++) {
		facto[i] = i * facto[i - 1] % MOD;

		ll sum = (dp[i - 1] + dp[i - 2]) % MOD;
		dp[i] = (i - 1) * sum % MOD;
	}
	cout << facto[N] * dp[N] % MOD<<"\n";
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/BOJ/14578.cpp)
- 