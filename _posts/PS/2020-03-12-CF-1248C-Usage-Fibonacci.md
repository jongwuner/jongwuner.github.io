---
layout:     post
title:      "Codeforces 1248C - Ivan the Fool and the Probability Theory"
subtitle:   "피보나치 규칙이 아직 잘 안보인다."
date:       2020-03-12 00:49:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Fibonacci
  - Find pattern
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76435477-5f4bd300-63fa-11ea-8e23-d9b21f8d8677.png)

<br><br><br><br><br>
## Approach
- 

## Solution


## Comment
- 피보나치 접근하는 팁? 
  - 이것을 항으로 바라보고, 이전꺼, 혹은 이전전꺼를 붙이는 작업이 보인다.
  - 써놓고도 애매.
- 파사노주기에 대한 공부?

## Code
```cpp
#include <bits/stdc++.h>
using namespace std;
 
 
long long fib[1000010], n, m, mod = 1000000007, res;
int main() {
	cin >> n >> m;
	fib[0] = 1;
	fib[1] = 1;
	for (int i = 2; i <= 100000; i++) {
		fib[i] = (fib[i - 1] + fib[i - 2]) % mod;
	}
	res = ((fib[n] + fib[m] - 1) * 2) % mod;
 
	cout << res << endl;
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1248C.cpp)
- 타일 채우기
- [ACM에 나왔던 피보나치 응용 - Message Passing](https://www.acmicpc.net/problem/13328)