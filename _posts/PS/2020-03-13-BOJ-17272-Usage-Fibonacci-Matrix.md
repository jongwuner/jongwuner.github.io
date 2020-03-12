---
layout:     post
title:      "BOJ 17271/17272 - 리그 오브 레전설(small/large)"
subtitle:   "피보나치 행렬로 N이 큰 문제에 대해서 분할정복으로 점화식 접근하기"
date:       2020-03-12 00:49:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Fibonacci
  - Divide & concur
  - DP
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76542870-0139f100-64c9-11ea-8b18-33644927d28c.png)
![image](https://user-images.githubusercontent.com/16419202/76542912-14e55780-64c9-11ea-82df-91142c7c1ab0.png)


<br><br><br><br><br>
## Approach
- 피보나치 DP스럽게 생각하면 좋다. `DP[i] = DP[i - 1] + DP[i - M]`

## Solution
- 1차원 DP로는 N의 크기가 10,000,000보다 큰 값을 해결하긴 어렵다.
- 이것보다 커질 때는, 점화식을 짠 뒤 `Fibonacci Matrix`로 해결해야 한다.  

## Comment
- 점화식부터 짠 뒤, N의 사이즈를 고려해야 한다.
- `Fibonacci Matrix`는 내가 얻은 점화식에 따라서 1행의 구성을 잘해야 한다. 

## Code
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
typedef vector<vector<ll>> Matrix;
const ll mod = 1000000007;
ll n, m;
Matrix bm;
Matrix ansMat;
Matrix Mult (Matrix a, Matrix b){
	Matrix ans(m + 1, vector<ll>(m + 1));
	for (int i = 1; i <= m; i++) 
		for (int j = 1; j <= m; j++) 
			for (int k = 1; k <= m; k++) 
				ans[i][j] = (ans[i][j] + (a[i][k] * b[k][j] % mod)) % mod;
	return ans;
}

Matrix getAnswer(ll N) {
	if (N == 1) return bm;
	Matrix tmpMatrix = getAnswer(N / 2);
	Matrix ans = Mult(tmpMatrix, tmpMatrix);
	if (N & 1) ans = Mult(ans, bm);
	return ans;
}
int main() {
	ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0);

	cin >> n >> m;
	bm.resize(m + 1, vector<ll>(m + 1, 0));
	bm[1][1] = bm[1][m] = 1;
	for (int i = 1; i < m; i++)
		bm[i + 1][i] = 1;
	ansMat = getAnswer(n);
	cout << ansMat[1][1] << "\n";
	return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/BOJ/17272.cpp)
- [Small 버전 코드](https://github.com/jongwuner/ps-study/blob/master/exercise/BOJ/17271.cpp)
- [Message Passing - 점화식 구성만 다르고 다 같음](https://github.com/jongwuner/ps-study/blob/master/exercise/BOJ/13328.cpp)