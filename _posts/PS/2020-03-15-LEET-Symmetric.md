---
layout:     post
title:      "Leetcode - Symmetric Tree"
subtitle:   "Symmetric Tree, Recursion 설계할 때, 가져가야 할 인자"
date:       2020-03-15 01:49:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Recursion
  - Tree
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76695526-f8613f00-66c3-11ea-81c9-20a45b1a7025.png)
![image](https://user-images.githubusercontent.com/16419202/76695529-02833d80-66c4-11ea-915e-d28378cbaf54.png)



<br><br><br><br><br>
## Approach
- Recursion 구조로 보이지가 않아서, 
- BFS식으로 구현하려 했으나, Library의 제약이 있어서 하지 못했다.

## Solution
- `Tree* Root1, Tree* Root2` 를 두 개 인자로 받아서 동시에 `pre-order` 할 수 있었다.

## Comment
- Recursion 설계의 자신감이 필요하다. 
- 아주 기본적인 것 부터(완전탐색, 중복순열, 중복조합, Top-down DP)

## Code
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */


class Solution {
public:
    
    bool isSymmetric(TreeNode* root) {
        return isMirror(root, root);
    }
    bool isMirror(TreeNode* a, TreeNode* b){
        if(a == NULL && b == NULL) return true;
        if(a == NULL || b == NULL) return false;
        return (a->val == b->val) && isMirror(a->left, b->right) && isMirror(a->right, b->left);
    }
};
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Leetcode/symmetric-tree.cpp)
- 완전탐색(중복순열, 중복조합 등등)