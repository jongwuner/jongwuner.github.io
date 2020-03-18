---
layout:     post
title:      "Leetcode - 3Sum"
subtitle:   "Three Pointer, Set의 사용"
date:       2020-03-18 22:04:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Two pointer
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76960841-a0466900-695f-11ea-878f-847ff92cc793.png)



<br><br><br><br><br>
## Approach
- Three Pointer과 Set의 사용

## Solution
- `AC`

## Comment
- Three Pointer는 모든 경우를 본다????
  - 맞다. `Pair ans = {a, b}가 존재한다고 가정할 때, k1,  k2,  k3,  a, k4, k5, k6, b, k7, k8 이 있다. a + b = k일 때, 최초 k1 + k8 > k일 경우, k1은 a쪽으로 갈 것, 
  k1 + k8 < k일 경우, k8이 b쪽으로 갈 것, L = a일 경우, 항상 a + b < a + k8 이다. a는 움직일 일이 없으므로 답을 찾게 된다.     


## Code
```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> vvi;
        set<tuple<int, int, int>> SET;


        sort(nums.begin(), nums.end());
        int N = nums.end() - nums.begin();
        for (int i = 0; i < N; i++) {
            int L = i + 1, R = N - 1;
            if (N <= L || N <= R) continue;
            while (L < R) {
                if (nums[i] + nums[L] + nums[R] < 0)
                    L++;
                else if (nums[i] + nums[L] + nums[R] > 0)
                    R--;
                else if (nums[i] + nums[L] + nums[R] == 0) {

                    if (SET.find({ nums[i], nums[L], nums[R] }) == SET.end()) {
                        vector<int> vi;
                        vi.push_back(nums[i]);
                        vi.push_back(nums[L]);
                        vi.push_back(nums[R]);
                        vvi.push_back(vi);
                        SET.insert({ nums[i], nums[L], nums[R] });

                    }

                    L++; R--;

                }
            }
        }
        return vvi;
    }
};
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Leetcode/3sum.cpp)
- 투 포인터, 쓰리 포인터가 모든 경우를 보는 것인가?