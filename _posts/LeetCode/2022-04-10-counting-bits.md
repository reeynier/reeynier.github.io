---
layout: post
title: "Counting Bits Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming, Bit Manipulation ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 338. Given an integer n, return an array ans of length n + 1 such that for each i (0 <= i <= n), ans[i] is the number of 1's in the binary representation of i.

---

<br />

## Description

LeetCode Problem 338.

Given an integer n, return an array ans of length n + 1 such that for each i (0 <= i <= n), ans[i] is the number of 1's in the binary representation of i.

Example 1:
```
Input: n = 2
Output: [0,1,1]
Explanation:
0 --> 0
1 --> 1
2 --> 10
```

Example 2:
```
Input: n = 5
Output: [0,1,1,2,1,2]
Explanation:
0 --> 0
1 --> 1
2 --> 10
3 --> 11
4 --> 100
5 --> 101
```

Constraints:
* 0 <= n <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> ans;
        
        ans.push_back(0);
        if (num == 0)
            return ans;
        
        int b = 0, e = 1;
        
        for (int i = 1; i <= num; i ++) {
            ans.push_back(ans[b] + 1);
            b ++;
            if (b == e) {
                b = 0;
                e = i + 1;
            }
        }
        return ans;
    }
};
```


