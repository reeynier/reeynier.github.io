---
layout: post
title: "Palindromic Substrings Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 647. Given a string s, return the number of palindromic substrings in it.

---

<br />

## Description

LeetCode Problem 647.

Given a string s, return the number of palindromic substrings in it.

A string is a palindrome when it reads the same backward as forward.

A substring is a contiguous sequence of characters within the string.

Example 1:
```
Input: s = "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```

Example 2:
```
Input: s = "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
```

Constraints:
* 1 <= s.length <= 1000
* s consists of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int countSubstrings(string s) {
        int n = s.size(), cnt = 0;
        vector<vector<int>> dp(n, vector<int>(n, 0));
        
        for (int k = 0; k < n; k ++) {
            for (int i = 0; i < n-k; i ++) {
                int j = i + k;
                if (k == 0) {
                    dp[i][j] = 1;
                }
                else if (k == 1) {
                    dp[i][j] = (s[i] == s[j]);
                } else {
                    if (dp[i+1][j-1] == 1 && s[i] == s[j]) {
                        dp[i][j] = 1;
                    } else {
                        dp[i][j] = 0;
                    }
                }
                cnt += dp[i][j];
                
            }
        }
        return cnt;
    }
};
```


