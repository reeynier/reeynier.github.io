---
layout: post
title: "Is Subsequence Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Two Pointers, Dynamic Programming, String ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 392. Given two strings s and t, return true if s is a subsequence of t, or false otherwise.

---

<br />

## Description

LeetCode Problem 392.

Given two strings s and t, return true if s is a subsequence of t, or false otherwise.
A subsequence of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., "ace" is a subsequence of "abcde" while "aec" is not).

Example 1:
```
Input: s = "abc", t = "ahbgdc"
Output: true
```

Example 2:
```
Input: s = "axc", t = "ahbgdc"
Output: false
```

Constraints:
* 0 <= s.length <= 100
* 0 <= t.length <= 10^4
* s and t consist only of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int m = s.size();
        int n = t.size();
        int dp[m + 1][n + 1];
        
        for (int i = 0; i <= m; i ++) {
            for (int j = 0; j <= n; j ++) {
                dp[i][j] = 0;
            }
        }
        
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                if (s[i] == t[j]) {
                    dp[i + 1][j + 1] = dp[i][j] + 1;
                } else {
                    dp[i + 1][j + 1] = dp[i + 1][j];
                }
            }
        }
                
        return (dp[m][n] == m);
    }
};
```


