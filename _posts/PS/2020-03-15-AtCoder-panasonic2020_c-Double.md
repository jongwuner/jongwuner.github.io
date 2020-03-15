---
layout:     post
title:      "AtCoder panasonic2020_c - Sqrt Inequality"
subtitle:   "Double의 오차, 정수형으로 바꿔서 풀 수 있는 방법을 항상 간구하자."
date:       2020-03-15 01:49:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Double
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76696189-ed121180-66cb-11ea-994e-8aeeff22df32.png)
![image](https://user-images.githubusercontent.com/16419202/76696192-f7341000-66cb-11ea-9bcb-0c292d83265a.png)



<br><br><br><br><br>
## Approach
- 단순히 식이 나타내는 대로 풀이했으나, 역대급 맞왜틀

## Solution
- Double에서 발생하는 소수점 오차때문에 계속 틀린 것으로 추정.
- 정수범위에서 문제풀 수 있도록, 4제곱했어야 한다.

## Comment
- 앞으로 이 문제는 잊을 수 없게 되었다.

## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
ll a, b, c;
int main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);

	cin >> a >> b >> c;
	ll x = c - a - b;
	if (x < 0) cout << "No\n";
	else if (4 * a * b < x * x) cout << "Yes\n";
	else cout << "No\n";

	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/AtCoder/panasonic2020_c.cpp)