---
layout:     post
title:      "Codeforces 1301C - Ayoub's Function"
subtitle:   "중앙에 고르게 펼쳐놓기, N, M으로 점화식 짜기, 0과 1"
date:       2020-03-12 00:49:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Explicit Formula
  - Find pattern
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76434384-f4e66300-63f8-11ea-83e3-bedae2e14116.png)
![image](https://user-images.githubusercontent.com/16419202/76434431-02035200-63f9-11ea-9a2d-9af72616dc6e.png)

<br><br><br><br><br>
## Approach
- 변수 2개를 주고, 규칙을 파악해야 하니, 변수 2개를 통해 점화식을 짜는게 맞다고 생각했다.
- 패턴을 찾다가, 홀짝으로 달라진다는 사실
- N이 증가할 때, 
- M이 증가할 때,
- 불균형이 왼쪽, 중앙, 오른쪽에 생길 때 차이점? 

## Solution
- 변수 2개로 짜는 점화식이 맞다.
- (N - M) / (M+1)
  - N은 순열의 최대 길이
  - M은 1인 수, (중간에 고르게 펼쳐져있다.)
  - (N - M)은 전체 순열에서 1을 제거하니 0의 개수이다.
  - (N - M)을 M+1의 구간으로 나눈다.
  - 몫과 나머지를 통해 답을 구할 수 있다.

## Comment
- 0과 1이 나올 때, 전사건과 여사건과 같은 느낌으로 활용하여 구할 수 있다.

## Code
```cpp
#include <cstdio>
 
long long n,m;
 
long long f(long long x) {
   return (x*x+x)/2;
}
 
int main(void) {
   int c;
   scanf("%d\n",&c);
   for(int t=0;t<c;t++) {
      scanf("%lld %lld\n",&n,&m);
      long long wid=(n-m)/(m+1);
      long long left=(n-m)%(m+1);
      printf("%lld\n",f(n)-left*f(wid+1)-(m+1-left)*f(wid));
   }
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1301C.cpp)
- [점화식 - 수학(1)]()
- [점화식 - 수학(2)]()
- [점화식 - 수학(3)]()
- [점화식 - DP(1)]()
- [점화식 - DP(2)]()
- [점화식 - DP(3)]()