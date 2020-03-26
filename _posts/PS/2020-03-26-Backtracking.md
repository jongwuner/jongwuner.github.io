---
layout:     post
title:      "boj 16637 - 괄호 추가하기"
subtitle:   "Recursion Tree"
date:       2020-03-26 22:34:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Recursion Tree
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/77657717-0747cb80-6fb9-11ea-8cd0-d5df812b0ba4.png)
![image](https://user-images.githubusercontent.com/16419202/77657810-247c9a00-6fb9-11ea-932e-b949ce7564bb.png)
![image](https://user-images.githubusercontent.com/16419202/77657861-38c09700-6fb9-11ea-9b0e-46b7da773c48.png)

<br><br><br><br><br>
## Approach
- DP인줄 알았는데, 문제의 선입견 때문임. -> 문제를 보고 사고를 하자. 외운 유형을 떠올리지 말고.

## Solution
- `AC`

## Comment
- Return이 있느냐 없느냐에 따른 차이. 
  - Return이 있다는 것은 ???
     - 적어도 Top-down DP라면 return이 있어야 한다. 
  - Return이 없다는 것은 완전탐색, 백트래킹. 
     - Level에 도달한 모든 경우 탐색해서, 최댓값, 최솟값 고르는 것. 
 

## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
int Ssize, ans = -1e9; string S;
int cal(int a, int b, char opt) {
	if (opt == '+') return a + b;
	if (opt == '-') return a - b;
	if (opt == '*') return a * b;
}
void getAnswer(int lev, int val) {
	if (lev == Ssize - 1) {
		ans = max(ans, val);
		return;
	}

	int v1, v2;
	v1 = cal(val, S[lev + 2] - '0', S[lev + 1]);
	getAnswer(lev + 2, v1);

	if (lev + 4 < Ssize) {
		v2 = cal(S[lev + 2] - '0', S[lev + 4] - '0', S[lev + 3]);
		v2 = cal(val, v2, S[lev + 1]);
		getAnswer(lev + 4, v2);
	}
}
int main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);

	cin >> Ssize >> S;
	getAnswer(0, S[0] - '0');
	cout << ans << "\n";
	return 0;
}
```

## Reference