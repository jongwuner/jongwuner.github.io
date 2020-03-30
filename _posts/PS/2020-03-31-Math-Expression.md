---
layout:     post
title:      "boj 1011 - Fly me to the Alpha Center"
subtitle:   "규칙발견, 패턴파악하고 점화식으로 정리, 이 때 Index 혼동하는 것"
date:       2020-03-26 22:34:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Math
  - Expression
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/77928764-c8c94e00-72e3-11ea-833e-2065a0fd4b9f.png)
![image](https://user-images.githubusercontent.com/16419202/77928811-d7b00080-72e3-11ea-8def-85581f348b61.png)


<br><br><br><br><br>
## Approach
- 처음에 문제를 잘못 읽고 `1 2 3 4 1` 이런식의 패턴도 가능하다고 생각했는데 그게 아니었다. 문제를 잘못 읽었다.
- ` 1 2 3  ... 3 2 1 ` 이런 식으로 진행되기 때문에 `N(N + 1) > LEN` 이런 식.
- 수식의 의미를 중도에 잃어버리는 실수는 아직까지 하고 있다. `부등호` 

## Solution
- `AC`

## Comment
- 수식의 의미를 잃어버린다.
- 점화식의 인덱스 혼동. i와 i-1을 활용하는 것도 있고, 
- 점화식의 항으로 예시 드는 연습. (그대로 멈춰있지 말자)


## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
int main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);

	int T; cin >> T; while (T--) {
		ll A, B, N = 0, add = 0;
		cin >> A >> B;
		while (N * (N + 1) < B - A) {
			N++;
		}
		if (N * (N - 1) + N < B - A) {
			add+=2;
		}
		else {
			add++;
		}
		N--;
		cout << 2*N + add<< "\n";
	}
	return 0;
}
```

## Reference
-[Github](https://github.com/jongwuner/ps-study/blob/master/exercise/BOJ/1011.cpp)