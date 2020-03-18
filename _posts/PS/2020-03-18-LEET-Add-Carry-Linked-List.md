---
layout:     post
title:      "Leetcode - Add Two Numbers"
subtitle:   "Carry, Linked List"
date:       2020-03-18 22:04:00
author:     "jjongwuner"
header-img: "img/post-bg-re-vs-ng2.jpg"
header-mask: 0.3
catalog:    true
categories: PS
tags:
  - Linked list
  - while
---

## Problem
![image](https://user-images.githubusercontent.com/16419202/76978978-b4e42a80-697a-11ea-8c98-a603566bb3d1.png)



<br><br><br><br><br>
## Approach
- carry을 활용하여, 다음 node의 계산값을 결정한다.

## Solution
- `AC`

## Comment
- while 문 설계 아직 미숙한 듯
- nextNode와 nowNode의 혼동

## Code
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* p = l1;
        ListNode* q = l2;
        ListNode* newNode = new ListNode((p->val + q->val) % 10);
        ListNode* head = newNode;

        int c = (p->val + q->val) / 10;
        
        while (p != NULL || q != NULL || c) {
            
            p = p->next;
            q = q->next;
            if (p == NULL && q == NULL && c == 0) break;
            if (p == NULL) p = new ListNode(0);
            if (q == NULL) q = new ListNode(0);

            ListNode* nextNode = new ListNode((p->val + q->val + c) % 10);
            c = (p->val + q->val + c) / 10;
            newNode->next = nextNode;
            newNode = nextNode;
        }
        return head;
    }
};
```

## Reference
- [Github](https://github.com/jongwuner/ps-study/blob/master/exercise/Leetcode/add-two-numbers.cpp)
- 조세퍼스 문제
- while 설계 
- 포인터 헷갈렸던 부분