---
layout:     post
title:      "BOJ 2624 - 동전 바꿔주기"
subtitle:   "Knapsack 응용문제, 기초"
date:       2020-03-15 01:49:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - DP
  - Knapsack
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76695560-6443a780-66c4-11ea-9e97-8f57640b9336.png)
![image](https://user-images.githubusercontent.com/16419202/76695566-702f6980-66c4-11ea-9a7b-b62091e1245d.png)



<br><br><br><br><br>
## Approach
- 동전의 개수를 처리해주는 것에 조금 오래걸렸다.

## Solution
- AC

## Comment
- knapsack 기본문제와 원리를 다시한번 뜯어봐야 할 듯하다.

## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef pair<int, int> Pair;
int T, N;
Pair coin[10005];
int dp[105][10005];
int main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
	
	cin >> T >> N;
	for (int i = 1; i <= N; i++) 
		cin >> coin[i].first >> coin[i].second;
	
	sort(coin + 1, coin + N + 1);
	
	dp[0][0] = 1;
	for (int i = 1; i <= N; i++) {
		for (int k = 0; k <= coin[i].second; k++) {
			for (int j = 0; j <= T; j++) {
				if (j + coin[i].first * k > T) continue;
				dp[i][j + coin[i].first * k] += dp[i - 1][j];
			}
		}
	}
	cout << dp[N][T] << "\n";
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/BOJ/2624.cpp)