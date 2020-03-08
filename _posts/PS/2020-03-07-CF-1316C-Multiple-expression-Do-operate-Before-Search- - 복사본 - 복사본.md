---
layout:     post
title:      "Codeforces 1316C - Primitive Primes"
subtitle:   "다항식의 계수 중 0이 아닌 것을 찾기(X자규칙), gcd(a1, a2, a3....) = gcd(b1, b2, b3...)"
date:       2020-03-07 14:04:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Expression
  - Find pattern
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76137139-bbba9580-607c-11ea-8e03-973371ea17bd.png)
![image](https://user-images.githubusercontent.com/16419202/76137144-ce34cf00-607c-11ea-8924-03027a87feec.png)

<br><br><br><br><br>
## Approach
- 최근에 풀었던 gcd로 오일러의 피함수 사용할 수 있는지
- X자 기준으로 차수가 같아진다는 것을 기준으로, 어떤 결과를 얻을 수 있는지
- 결국 알아내지 못함.

## Solution
- 다항식의 해당 차수가 유효하려면, 계수가 0이 아니어야 함.
- 계수가 0이 아니라는 것은 A와 B에 입력받는 값에 %p 연산의 결과를 넣어준다.
```
    0 0 0 0 0 a   ....
    0 0 0 b  ...............
```
- 처음 나오는 0이 아닌 a와 b값을 찾은 후에 a와 b 인덱스를 더해주면 그 해당 차수가 된다. 

## Comment
- 다항식에서 해당 차수인 계수를 찾는 문제는 이렇게 풀면 될 듯 하다.
- gcd는 필요한 조건이 아닌 듯 하다.
- 자료구조는 저장을 해서 내가 필요에 의해서(시간복잡도 고려) 조회를 다시 하기 위함이다. 
   - 내 입력받은 것을 다시는 쓸일이 없을 때, 저장할 필요가 없다.
   - 선형자료구조,  이값들을 재 확인할 때, 입력받는 순서가 보장되어야 한다.
   - PQ, 이 값들을 재 확인할때, 어떤 변수의 크기 순서대로 보장되어야 한다.
   - Q, 이 값들을 재 확인할때, 어떤 조건에 부합했던 순서대로
   - Stack, 이 값들을 재 확인할때, 가장 최근에 부합했던 순서대로


## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
int n, m, p, ans;
vector<int> a, b;
int main(){
	ios_base::sync_with_stdio(false); cin.tie(0); cout.tie(0);

	cin >> n >> m >> p;
	a.resize(n); b.resize(m);
	bool fg = false;
	for (int i = 0; i < n; i++) {
		cin >> a[i];
		a[i] %= p;
		if (!fg && a[i]) {
			fg = true;
			ans += i;
		}
	}
	fg = false;
	for (int i = 0; i < m; i++) {
		cin >> b[i];
		b[i] %= p;
		if (!fg && b[i]) {
			fg = true;
			ans += i;
		}
	}
	cout << ans << "\n";
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1316C.cpp)