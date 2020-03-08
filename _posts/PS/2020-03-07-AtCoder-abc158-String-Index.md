---
layout:     post
title:      "AtCoder abc158 D - String Formation"
subtitle:   "String을 Front, Back에서 Push하고 Reverse 시키는 Query 문제"
date:       2020-03-07 23:04:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - String
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76159567-6a3a0580-6165-11ea-9555-76f4d026f383.png)
![image](https://user-images.githubusercontent.com/16419202/76159571-76be5e00-6165-11ea-86b3-bcbfcc0626f6.png)
![image](https://user-images.githubusercontent.com/16419202/76159575-83db4d00-6165-11ea-88ed-a9fe607e8dd7.png)
![image](https://user-images.githubusercontent.com/16419202/76159583-935a9600-6165-11ea-94fe-274fe083d36d.png)


<br><br><br><br><br>
## Approach
- 처음에 String Reverse하는게 오래걸릴 것 같다는 판단을 했으므로, 홀짝규칙으로 reverse 상태인지 아닌지를 판단해서 앞뒤 중 어디에 넣어줄지 판단을 했다.
- String ts변수를 생성하고, input하는 변수를 넣은 후, 기존 string을 더했다.
- 이렇게 했는데도 불구하고 계속 시간초과가 났다.
- 한참뒤에 Q는 2*10**6 개가 들어올 수 있어서, 최종 |S|은 3*10**6이 된다는걸 깨달았다. 
- startPoint와 endPoint를 이 구간의 중간으로 초기화하니까 `AC` 받았다.

## Solution
- AC

## Comment
- 디버깅 하면서 한 부분씩 코드를 수정할 때 주의할 점은, 기존코드에 범위(오버플로우)나, 생성한 변수의 크기 등을 고려해야 한다.
- startPoint는 첫부분을 가리키고 있고, endPoint는 이제 새로 들어올 부분을 가리키고 있다. 이런 규칙을 본인이 헷갈려하지 말자.
- String 변수를 사용하는 문제에서는 0인덱스 어떤식으로 유의할지 고민해보자. 많이 혼동되는 것 같다.

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
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/AtCoder/abc158_d.cpp)