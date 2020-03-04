---
layout:     post
title:      "Codeforces Div2 624 1295D - Same GCDs"
subtitle:   "오일러의 피함수 이용."
date:       2020-02-28 21:04:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Math
  - Euler's Function
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/75769100-e6f56a00-5d88-11ea-8a92-90ee2773fb54.png)

<br><br><br><br><br>
## Approach
- a, a+x사이에 있는 소수를 검사하는 방식으로 진행했다. 
- a, a+x사이에 있는 숫자를 소인수분해 생각을 했었는데, 시간복잡도로 인해 솔루션을 찾지 못했다.

## Solution
- 다음의 글을 이해해야 한다.<br>

```
if(a + x > m)이면서  gcd(a + x, m) = gcd(a, m)일 때,
gcd(a + x - m, m) = gcd(a, m)이고,
x' = (a + x) mod m 이라는 것을 알 수 있음.
0 <= x' < m 이며,

gcd(x', m) = gcd(a, m) = gcd(gx'', gm') = g * gcd(x'', m')이다. [gcd(x'', m') == 1]
 x' = gx''
2  = 2 * 1
m = gm' 이다. m / g = m'
4 = 2 * 2
그러므로, m'와 0 <= x < m', x는 m'와 서로소인 갯수를 구하면 된다.
why? gcd(x'', m') == 1이고, 그러한 x''의 갯수를 구하면 되는 것.
x''의 또한 0 <= x'' < m'
```
<br>
## Comment
- `오일러의 피함수`를 쓰도록 저 위처럼 유도하는 과정.
- `모듈러스 연산`은 gcd(a + x, m)  == gcd(a + x - m, m) == gcd(a + x - 2*m, m) 이렇다는 것을 깨닫자. 
- 구현코드를 잘 알아두자.

## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
ll A, M;
ll gcd(ll a, ll b) {
	if (b == 0)return a;
	return gcd(b, a % b);
}
ll phi(ll n) {
	ll res = n;
	for (ll i = 2; i * i <= n; i++) {
		if (n % i) continue;
		res -= res / i;
		while (n % i == 0)
			n /= i;
	}
	if (n > 1)
		res -= res / n;
	return res;
}
int main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);

	int T; cin >> T; while (T--) {
		cin >> A >> M;
		ll G = gcd(A, M);
		ll M2 = M / G;
		cout << phi(M2) << "\n";
	}
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1295D.cpp)
- [Gcd 이용 - (1)]()
- [Gcd 이용 - (2)]()
- [Gcd 이용 - (3)]()