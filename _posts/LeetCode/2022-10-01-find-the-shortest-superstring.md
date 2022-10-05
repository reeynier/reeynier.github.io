---
layout: post
title: "Find The Shortest Superstring Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, String, Dynamic Programming, Bit Manipulation, Bitmask ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 943. Given an array of strings words, return the smallest string that contains each string in words as a substring. If there are multiple valid strings of the smallest length, return any of them.

---

<br />

## Description

LeetCode Problem 943.

Given an array of strings words, return the smallest string that contains each string in words as a substring. If there are multiple valid strings of the smallest length, return any of them.

You may assume that no string in words is a substring of another string in words.

Example 1:
```
Input: words = ["alex","loves","leetcode"]
Output: "alexlovesleetcode"
Explanation: All permutations of "alex","loves","leetcode" would also be accepted.
```

Example 2:
```
Input: words = ["catg","ctaagt","gcta","ttca","atgcatc"]
Output: "gctaagttcatgcatc"
```

Constraints:
* 1 <= words.length <= 12
* 1 <= words[i].length <= 20
* words[i] consists of lowercase English letters.
* All the strings of words are unique.

<br />

## Sample C++ Code


```c
class Solution {
public: 
    string shortestSuperstring(vector<string>& A) {
        const int n = A.size();
        vector<vector<int> > g(n, vector<int>(n));
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++) {
                g[i][j] = A[j].length();
                for (int k = 1; k <= min(A[i].length(), A[j].length()); k++) {
                    if (A[i].substr(A[i].length()- k) == A[j].substr(0, k)) {
                        g[i][j] = A[j].length() - k;
                    }
                }
            }
        
        vector<vector<int> > dp(1<<n, vector<int>(n, INT_MAX/2));
        vector<vector<int> > parent(1<<n, vector<int>(n, -1));
        for (int i = 0; i < n; i++) 
            dp[1<<i][i] = A[i].length();  
        
        for (int s = 1; s < (1<<n); s++) {
            for (int j = 0; j < n; j++) {
                if (!s & (1 << j)) 
                    continue;
                int ps = s & ~(1 << j);
                for (int i = 0; i < n; i++) {
                    if (dp[s][j] > dp[ps][i] + g[i][j]) {
                        dp[s][j] = dp[ps][i] + g[i][j];
                        parent[s][j] = i;
                    }
                }
            }
        }
        
        string res;
        auto it = min_element(begin(dp.back()), end(dp.back()));
        int j = it - begin(dp.back()); 
        int s = (1 << n) - 1;
        while (s) {
            int i = parent[s][j]; 
            if (i < 0) 
                res = A[j] + res;
            else 
                res = A[j].substr(A[j].length() - g[i][j]) + res;            
            s &= ~(1 << j);
            j = i;
        }
        return res;        
    }
};
```


