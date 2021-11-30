---
layout: post
title: "Distinct Subsequences Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 115. Given two strings s and t, return the number of distinct subsequences of s which equals t.

---

<br />

## Description

LeetCode Problem 115.

Given two strings s and t, return the number of distinct subsequences of s which equals t.

A string's subsequence is a new string formed from the original string by deleting some (can be none) of the characters without disturbing the remaining characters' relative positions. (i.e., "ACE" is a subsequence of "ABCDE" while "AEC" is not).

The test cases are generated so that the answer fits on a 32-bit signed integer.

Example 1:
```
Input: s = "rabbbit", t = "rabbit"
Output: 3
Explanation:
As shown below, there are 3 ways you can generate "rabbit" from S.
rabbbit
rabbbit
rabbbit
```

Example 2:
```
Input: s = "babgbag", t = "bag"
Output: 5
Explanation:
As shown below, there are 5 ways you can generate "bag" from S.
babgbag
babgbag
babgbag
babgbag
babgbag
```

Constraints:
* 1 <= s.length, t.length <= 1000
* s and t consist of English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
	// Define dp[i][j] to be the number of distinct subsequences 
	// of t[0..i - 1] in s[0..j - 1]. Then we have the following state equations:
	// General case 1: dp[i][j] = dp[i][j - 1] if t[i - 1] != s[j - 1];
	// General case 2: dp[i][j] = dp[i][j - 1] + dp[i - 1][j - 1] if t[i - 1] == s[j - 1];
	// Boundary case 1: dp[0][j] = 1 for all j;
	// Boundary case 2: dp[i][0] = 0 for all positive i.
    int numDistinct(string s, string t) {
        int m = t.length(), n = s.length();
        vector<vector<int>> dp(m + 1, vector<int> (n + 1, 0));
        for (int j = 0; j <= n; j++) dp[0][j] = 1;
        for (int j = 1; j <= n; j++)
            for (int i = 1; i <= m; i++)
                dp[i][j] = dp[i][j - 1] + (t[i - 1] == s[j - 1] ? dp[i - 1][j - 1] : 0);
        return dp[m][n];
    }
};  
```


