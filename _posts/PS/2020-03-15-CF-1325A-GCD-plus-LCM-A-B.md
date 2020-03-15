---
layout:     post
title:      "Codeforces 1325A - EnAb AnD gCd"
subtitle:   "GCD와 LCM의 합으로 A, B 쌍을 찾기"
date:       2020-03-15 01:49:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - GCD
  - LCM
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76695502-b3d5a380-66c3-11ea-9498-130ac4fca020.png)


<br><br><br><br><br>
## Approach
- ★고민의 시간을 많이 사용
- 설계할 때, `직접해봐야 하나?? 빠른 방법이 있나??` 12분 걸려서 풀이함.
- `gcd(1 + a'b')` 고 a'b'도 직접찾음. 

## Solution
- 직접 찾는 것도 답. 첫번째 반복문에서 탈출하게 됌.
- gcd를 1로 잡고, a'b' = N - 1이니까, `print (1, N - 1)` 출력.

## Comment
- 변수가 헷갈려서 시간이 좀더 걸린 것 같기도 하다.
  - 내가 지금 구해야하는 것이 무엇인지?
  - `gcd*a', gcd*b` 인데, gcd가 1이니까 a'b' 구하면 된다.
  - a'b'는 N - 1이니까 가장 간단한 a' = 1, b' = N - 1
  - `print (1, N-1)`

- 변수가 헷갈려서, 무엇을 구하고자 하는지 까먹는 유형

## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
ll N, A, B, GCD;
int gcd(int a, int b) {
	if (b == 0)return a;
	return gcd(b, a % b);
}
int main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);
 
	int T; cin >> T; while (T--) {
		cin >> N;
		for (int i = 1; i * i <= N; i++) {
			if (N % i) continue;
			int tmp = N / i - 1;
			for (int j = 1; j * j <= tmp; j++) {
				if (tmp % j) continue;
				A = j;
				B = tmp / j;
				GCD = i;
				break;
			}
		}
		cout << GCD*A << " " << GCD*B << "\n";
	}
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1325A.cpp)