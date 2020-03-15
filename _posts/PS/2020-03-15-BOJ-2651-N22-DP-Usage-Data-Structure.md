---
layout:     post
title:      "BOJ 2651 - 자동차경주대회"
subtitle:   "N**2 DP, 자료구조 선정(1차원, 2차원)"
date:       2020-03-15 01:49:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - DP
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76695533-1d55b200-66c4-11ea-8ade-a40302a6acd5.png)
![image](https://user-images.githubusercontent.com/16419202/76695539-2b0b3780-66c4-11ea-8462-03eedede3070.png)


<br><br><br><br><br>
## Approach
- 규칙이 잘 보이지 않음.
- `Find pattern` 

## Solution
- 회문일 경우에 가운데에 한 개 더생기는 규칙
- 다음항으로 갈 때, 1->0, 0->1 바뀌는 규칙

## Comment
- 알고 Find pattern하자
- 지금 너무 까막눈이다. 

## Code
```cpp
#include <cstdio>

enum {m = 1000000000, size = 40};

class DP
{
public:
	int data[size];
	int power[size];

	DP()
	{
		for (int i = 0; i < size; i++)
			data[i] = power[i] =0;
		power[0] = 1;
	}

	void next()
	{
		int borrow = 0;
		for (int i = 0; i < size; i++)
		{
			data[i] = power[i] - data[i] - borrow;
			if (data[i] < 0)
			{
				data[i] += m;
				borrow = 1;
			}
			else
				borrow = 0;
		}

		int carry = 0;
		for (int i = 0; i < size; i++)
		{
			long long tmp = (long long)power[i] * 2 + carry;
			if (tmp >= m)
			{
				tmp -= m;
				carry = 1;
			}
			else
				carry = 0;
			power[i] = tmp;
		}
	}

	void print()
	{
		int i = size -1;
		while (data[i] == 0)
			i--;

		printf("%d", data[i--]);
		while (i >= 0)
			printf("%09d", data[i--]);
		printf("\n");
	}

};

int main()
{
	int n;
	scanf("%d", &n);
	DP dp;

	for (int i = 1; i < n; i++)
		dp.next();
	
	if (n == 1)
	{
		printf("0\n");
		return 0;
	}

	dp.print();
	
}

/*
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
ll N;
pair<ll, ll> now = {0, 1};
//now.first : 0
//now.second : 1
int main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
	cin >> N;
	for (int i = 2; i <= N; i++) {
		ll tmp = now.first;
		now.first += now.second;
		now.second += tmp;
		if (i & 1) {
			now.first -= 1;
		}
	}
	cout << now.first << "\n";
	return 0;
}
*/
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/BOJ/2651.cpp)
- [비슷한 문제 - 운전면허시험](https://www.acmicpc.net/problem/10251)