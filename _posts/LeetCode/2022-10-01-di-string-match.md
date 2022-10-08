---
layout: post
title: "DI String Match Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Two Pointers, String, Greedy ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 942. A permutation perm of n + 1 integers of all the integers in the range [0, n] can be represented as a string s of length n where

---

<br />

## Description

LeetCode Problem 942.

A permutation perm of n + 1 integers of all the integers in the range [0, n] can be represented as a string s of length n where:
* s[i] == 'I' if perm[i] < perm[i + 1], and
* s[i] == 'D' if perm[i] > perm[i + 1].

Given a string s, reconstruct the permutation perm and return it. If there are multiple valid permutations perm, return any of them.

Example 1:
```
Input: s = "IDID"
Output: [0,4,1,3,2]
```

Example 2:
```
Input: s = "III"
Output: [0,1,2,3]
```

Example 3:
```
Input: s = "DDI"
Output: [3,2,0,1]
```

Constraints:
* 1 <= s.length <= 10^5
* s[i] is either 'I' or 'D'.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> diStringMatch(string S) {
        int n = S.size();
        vector<int> ans(n+1, 0);
        
        int p = 0, q = n;
        for (int i = 0; i < n; i ++) {
            if (S[i] == 'I') {
                ans[i] = p;
                p ++;
            } else {
                ans[i] = q;
                q --;
            }
        }
        ans[n] = p;
        
        return ans;
    }
};
```


