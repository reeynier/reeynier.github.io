---
layout: post
title: "Longest Palindromic Subsequence Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 516. Given a string s, find the longest palindromic subsequence's length in s.

---

<br />

## Description

LeetCode Problem 516.

Given a string s, find the longest palindromic subsequence's length in s.

A subsequence is a sequence that can be derived from another sequence by deleting some or no elements without changing the order of the remaining elements.

Example 1:
```
Input: s = "bbbab"
Output: 4
Explanation: One possible longest palindromic subsequence is "bbbb".
```

Example 2:
```
Input: s = "cbbd"
Output: 2
Explanation: One possible longest palindromic subsequence is "bb".
```

Constraints:
* 1 <= s.length <= 1000
* s consists only of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int longestPalindromeSubseq(string s) {
        int n = s.size();
        vector<vector<int>> dp(n+1,vector<int>(n));
        
        for (int i = 0; i < n; i++) 
            dp[1][i] = 1;
        for (int i = 2; i <= n; i++) 
            for (int j = 0; j < n-i+1; j++) 
                dp[i][j] = (s[j]==s[i+j-1]) ? (2 + dp[i-2][j+1]) : max(dp[i-1][j], dp[i-1][j+1]);
        
        return dp[n][0]; 
    }
};
```


