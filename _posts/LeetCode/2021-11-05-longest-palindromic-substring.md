---
layout: post
title:  "Longest Palindromic Substring Problem"
categories: [ Algorithm ]
tags: [ Dynamic Programming, Leetcode ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 5. Given a string s, return the longest palindromic substring in s.
---

<br />

## Description

LeetCode Problem 5. 

Given a string s, return the longest palindromic substring in s.


Example 1:
```
Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

Example 2:
```
Input: s = "cbbd"
Output: "bb"
```

Example 3:
```
Input: s = "a"
Output: "a"
```

Example 4:
```
Input: s = "ac"
Output: "a"
```

Constraints:

* 1 <= s.length <= 1000
* s consist of only digits and English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.size();
        vector<vector<int>> dp(n, vector<int>(n, 0));
        
        int max_len = 0, idx_i = 0, idx_j = 0;
        for (int k = 0; k < n; k ++) {
            for (int i = 0; i < n-k; i ++) {
                int j = i+k;
                if (k == 0) {
                    dp[i][j] = 1;
                } else if (k == 1) {
                    dp[i][j] = (s[i] == s[j]);
                } else {
                    if (dp[i+1][j-1] == 1 && s[i] == s[j])
                        dp[i][j] = 1;
                    else 
                        dp[i][j] = 0;
                }
                
                if (dp[i][j] == 1) {
                    if (j-i+1 > max_len) {
                        max_len = j - i + 1;
                        idx_i = i;
                        idx_j = j;
                    }
                }
            }
        }
        
        return s.substr(idx_i, max_len);
    }
};
```
