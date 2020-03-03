---
layout:     post
title:      "Codeforces Educational Round 81 1295C - Obtain The String"
subtitle:   "Alphabet Key의 활용 -> DP[i][j] : lis[i]에(i < k <= lis.end) Alphabet 'j'가 있는 index "
date:       2020-02-28 17:04:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - DP
  - String
  - Alphabet Key
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/75766959-4e111f80-5d85-11ea-89a9-1953bb931e7c.png)

<br><br><br><br><br>
## Approach
- 정답의 sequnce를 선형탐색하면서, Map 자료구조로 입력/조회하면서 접근. 
- 중복되는 a,b


## Solution
- lis[idx] 을 볼 때, lis[idx - 1]와 lis[idx + 1] 둘 중 하나에 lis[idx]보다 하나 작은 알파벳이 있으면, lis[idx]를 제거한다. 

## Comment
- 완전탐색 시간복잡도 계산하는게 왜 어려웠을까? 
- z부터 a까지 지워가면, 지금 하는 선택이 이후에 하는 선택에 악영향(?)을 끼치지 않는다는 것을 알아야 한다.
  - lis[idx - 1]와 lis[idx + 1]까지 없애는 것이 아니었기 때문.
  - 가장 높은 알파벳 하나씩 제거하면, 이후의 선택에 그 다음 높은 알파벳들은 남아있기에 아무문제가 되지 않는다.
- 알파벳을 `Key`로 사용하게 되면 아주 유익한 순간들이 온다. 
- `lis.erase()`을 한 후에, `lis.mv()` 하기까지 시간이 오래걸리지 않는 다는 것을 깨달았어야 했다. 


## Code
```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
int n;
char a[105];
 
int main() {
    ios_base::sync_with_stdio(false); cin.tie(0);
    cin >> n >> a + 1;
    int rn = n;
    for (char i = 'z'; i > 'a'; i--) { 
        for (int go = 1; go <= 100; go++) {
            for (int j = 1; j <= n; j++) { 
                if (a[j] == i && (a[j - 1] == i - 1 || a[j + 1] == i - 1)) {
                    for (int k = j; k < n; k++) a[k] = a[k + 1];
                    a[n] = '!';
                    n--;
                    j--;
                }
            }
        }
    }
    cout << rn - n << '\n';
}
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1321C.cpp)
- [알파벳 Key 사용 - DP식, SubString](https://github.com/jongwuner/ps-study/blob/master/exercise/Codeforce/1295C.cpp)