---
layout:     post
title:      "Codeforces Round #619 1301D - Time To Run"
subtitle:   "구현이 가능하다면, 수식보다는 자료구조를 이용한 구현"
date:       2020-02-25 14:04:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Construction
  - Data Constructure
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/75770693-caa6fc80-5d8b-11ea-9a56-df2e8f6c6290.png)
![image](https://user-images.githubusercontent.com/16419202/75770713-d5fa2800-5d8b-11ea-94ca-76d141a3e5d6.png)
![image](https://user-images.githubusercontent.com/16419202/75770737-e3afad80-5d8b-11ea-9ef7-4cb02c5fa8dd.png)
![image](https://user-images.githubusercontent.com/16419202/75770759-f0cc9c80-5d8b-11ea-9481-8eb422aea46d.png)

<br><br><br><br><br>
## Approach
- 범위를 나눠서 모든 것을 수식으로 표현하려고 했음.
  - 등차수열 일반항 구하는 방식으로, k의 유효한 범위를 구하는 접근.
- TestCases는 잘 나왔으나, col의 값을 1을 입력받았을 때, `예외처리`하는 부분이 쉽지 않았다.


## Solution
- `Pair<Int, String>` 사용해서 모든 값을 넣어두고
- Pop하면서 수정하고, 
- Pop했다가 수정한 것 다시 Push하고, 
- 결과출력의 과정.


## Comment
- 그리드 간선그래프, 모든 간선을 방문하고 돌아올 수 있다. `한붓그리기 가능`

## Code
```cpp
#include <bits/stdc++.h>
using namespace std;
#define oo 1000000000
#define mod 998244853
const int N = 100010;

vector< pair< int, string > > v, v2;

int n, m, k, all = 0, cur;

string tmp;

void fix(vector< pair< int, string > >& v) {
    v2 = v;
    v.clear();
    for (int i = 0; i < (int)v2.size(); i++) {
        if (v2[i].first != 0)
            v.push_back(v2[i]);
    }
}

int main() {
    scanf("%d%d%d", &n, &m, &k);
    for (int i = 1; i <= n; i++) {
        v.push_back(make_pair(m - 1, "R"));
        all += (v.back().first * (int)v.back().second.size());
        if (i == 1)
            v.push_back(make_pair(m - 1, "L"));
        else
            v.push_back(make_pair(m - 1, "UDL"));
        all += (v.back().first * (int)v.back().second.size());
        if (i == n)
            v.push_back(make_pair(n - 1, "U"));
        else
            v.push_back(make_pair(1, "D"));
        all += (v.back().first * (int)v.back().second.size());
    }
    if (all < k) {
        puts("NO");
        return 0;
    }
    while (all > k) {
        tmp = v.back().second;
        cur = (v.back().first * (int)v.back().second.size());
        v.pop_back();
        all -= cur;
        if (all >= k)
            continue;
        cur = k - all;
        if (cur / (int)tmp.size() > 0) v.push_back(make_pair(cur / (int)tmp.size(), tmp));
        tmp.resize(cur % (int)tmp.size());
        if ((int)tmp.size() > 0) v.push_back(make_pair(1, tmp));
        all = k;
    }
    puts("YES");
    fix(v);
    printf("%d\n", (int)v.size());
    for (int i = 0; i < (int)v.size(); i++) {
        printf("%d %s\n", v[i].first, v[i].second.c_str());
    }
    return 0;
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1301D.cpp)