---
layout:     post
title:      "Codeforces Ozon Tech Challenge 1305C - Kuroni and Impossible Calculation"
subtitle:   "비둘기집 원리, Ai중에 같은 값이 있다면 "
date:       2020-03-04 04:23:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Pigeon Hall
  - Modulus
  - Math
  - Math-Simple
---

## Problem

<br><br><br><br><br>
## Approach
- Stack을 사용하는 구현 <- '('')' String의 전형적인 문제라고 떠올림.
- Queue를 사용하는 구현?
- 선형자료구조를 이용한(왼쪽에서부터의 '('개수, 오른쪽에서부터의 ')'개수) Construction
  - 문자열도 옮겨야 하는 문제발생. 
 
## Solution
- `Meet-In-The-Middle`이 제일 간단한 솔루션.
  - 가장 바깥의 왼쪽'(', 오른쪽')'부터 없애나가면 된다. 
- 결국 남는 것은 `)(` ,`))(((` 이런 식의 변형이기 때문에 마주보고 있는 `(` 와 `)`는 모두 없어진 결과이다. 
  
## Comment
- 물음에 답변해보자.
  - Ai을 M으로 나눈 나머지도 같이 고려를 해야하나??? 
    ex. N=3 M=6일때, a1 = 5, a2 = 11, a3 = 17, ... , 이런식의 반례는?? 
  - 일정하게 M의 차이를 내면 %값은 0이된다. 바로 결과값은 0이된다.
  - %값은 어차피 0 <= mod < M이기때문에, mod값을 가지게 되면, abs값은 0 <= mod < M값을 골고루 가지게 된다.
- 비둘기집 원리
- 수학적 원리와 규칙이 있었을까? 아니다, 복잡해보이는 식과 비둘기집원리를 이용해서 간단히 풀리는 문제였다.


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
- [Modulus 활용 - (1)](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1305C.cpp)
- [Pigeon Hall 활용 - (1)][]