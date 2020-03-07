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
  - Find Pattern(Not)
  - Find 
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/75814820-c1428200-5dd5-11ea-92d4-0f5534fbc5d7.png)

<br><br><br><br><br>
## Approach
- 전개식을 활용해서 수학적 규칙을 찾는거라고 생각했다. `뇌 비우고 규칙찾기`

## Solution
- 모듈러스 연산의 성질, 분배법칙 성립(덧셈, 뺄셈, 곱셈에 대해 성립) 
- a1 ~ an 사이에서 같은 나머지값이 한번이라도 나오면 결과는 0이 된다. 
- a1 ~ an 사이에서 나머지연산의 결과가 0이나오면 결과는 0이 된다.
- 그러면 0 < mod < M인데, M개의 나머지를 최대 한개씩 나눠 들어가야 한다. 
- if(N >= M) ans = 0 이 될수밖에 없다. 

## Comment
- 물음에 답변해보자.
  - Ai을 M으로 나눈 나머지도 같이 고려를 해야하나??? 
    ex. N=3 M=6일때, a1 = 5, a2 = 11, a3 = 17, ... , 이런식의 반례는?? 
  - 일정하게 M의 차이를 내면 %값은 0이된다. 바로 결과값은 0이된다.
  - %값은 어차피 0 <= mod < M이기때문에, mod값을 가지게 되면, abs값은 0 <= mod < M값을 골고루 가지게 된다.
- 모듈러스 연산의 성질을 알아두자.
![image](https://user-images.githubusercontent.com/16419202/75846447-adbc0900-5e1f-11ea-8ba2-a8f6b413d010.png)
- 비둘기집 원리
- 수학적 원리와 규칙이 있었을까? 아니다, 복잡해보이는 식과 비둘기집원리를 이용해서 간단히 풀리는 문제였다.
- 보여지는 N으로는 시간복잡도를 짤 수 없는 부분, 나머지연산 범위 M에 주목했어야 했다. 

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