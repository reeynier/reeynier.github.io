---
layout: post
title:  "Wildcard Matching Problem"
categories: [ Algorithm ]
tags: [ String, Dynamic Programming, Greedy, Recursion, Leetcode ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 44. Write the code that will take a string and make this conversion given a number of rows.
---

<br />

## Description

LeetCode Problem 44. 

Given an input string (s) and a pattern (p), implement wildcard pattern matching with support for '?' and '*' where:

* '?' Matches any single character.
* '*' Matches any sequence of characters (including the empty sequence).

The matching should cover the entire input string (not partial).
 

Example 1:
```
Input: s = "aa", p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```

Example 2:
```
Input: s = "aa", p = "*"
Output: true
Explanation: '*' matches any sequence.
```

Example 3:
```
Input: s = "cb", p = "?a"
Output: false
Explanation: '?' matches 'c', but the second letter is 'a', which does not match 'b'.
```

Example 4:
```
Input: s = "adceb", p = "*a*b"
Output: true
Explanation: The first '*' matches the empty sequence, while the second '*' matches the substring "dce".
```

Example 5:
```
Input: s = "acdcb", p = "a*c?b"
Output: false
```

Constraints:

* 0 <= s.length, p.length <= 2000
* s contains only lowercase English letters.
* p contains only lowercase English letters, '?' or '*'.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isMatch(string s, string p) {
        vector<vector<bool>> dp(s.size() + 1, vector(p.size() + 1, false));
        dp[0][0] = true;
        for (int j = 0; j < p.size() && p[j] == '*'; ++j) {
            dp[0][j + 1] = true;
        }
        
        for (int i = 1; i <= s.size(); ++i) {
            for (int j = 1; j <= p.size(); ++j) {
                if (p[j - 1] == '*') {
                    dp[i][j] = dp[i - 1][j] || dp[i][j - 1];
                } else {
                    dp[i][j] = (s[i - 1] == p[j - 1] || p[j - 1] == '?') && dp[i - 1][j - 1];
                }
            }
        }

        return dp[s.size()][p.size()];
    }
};
```
