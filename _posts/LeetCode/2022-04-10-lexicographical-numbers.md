---
layout: post
title: "Lexicographical Numbers Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Depth-First Search, Trie, Math ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 386. Given an integer n, return all the numbers in the range [1, n] sorted in lexicographical order.

---

<br />

## Description

LeetCode Problem 386.

Given an integer n, return all the numbers in the range [1, n] sorted in lexicographical order.
You must write an algorithm that runs inO(n)time and uses O(1) extra space.

Example 1:
```
Input: n = 13
Output: [1,10,11,12,13,2,3,4,5,6,7,8,9]
```

Example 2:
```
Input: n = 2
Output: [1,2]
```

Constraints:
* 1 <= n <= 5 * 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> lexicalOrder(int n) {
        vector<int> res(n);
        int cur = 1;
        for (int i = 0; i < n; i++) {
            res[i] = cur;
            if (cur * 10 <= n) {
                cur *= 10;
            } else {
                if (cur >= n) 
                    cur /= 10;
                cur += 1;
                while (cur % 10 == 0)
                    cur /= 10;
            }
        }
        return res;
    }
};
```


