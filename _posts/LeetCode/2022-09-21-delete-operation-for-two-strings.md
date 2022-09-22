---
layout: post
title: "Delete Operation For Two Strings Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 583. Given two strings word1 and word2, return the minimum number of steps required to make word1 and word2 the same.

---

<br />

## Description

LeetCode Problem 583.

Given two strings word1 and word2, return the minimum number of steps required to make word1 and word2 the same.

In one step, you can delete exactly one character in either string.

Example 1:
```
Input: word1 = "sea", word2 = "eat"
Output: 2
Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".
```

Example 2:
```
Input: word1 = "leetcode", word2 = "etco"
Output: 4
```

Constraints:
* 1 <= word1.length, word2.length <= 500
* word1 and word2 consist of only lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    /**
     * DP Formula: 
     * dp[i][j] = a[i] == b[j] ? dp[i + 1][j + 1] :
     *            min(1 + dp[i + 1][j],  // delete a[i] + mindist between a.substr(i+1), b.substr(j)
     *                1 + dp[i][j + 1])  // delete b[j] + mindist between a.substr(i), b.substr(j+1)
     */
    int minDistance(string a, string b) {
        int m = a.size(), n = b.size();
        vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
        for (int i = m; i >= 0; i--) {
            for (int j = n; j >= 0; j--) {
                if (i < m || j < n)
                    dp[i][j] = i < m && j < n && a[i] == b[j] ?
                        dp[i + 1][j + 1] : 1 + min((i < m ? dp[i + 1][j] : INT_MAX), (j < n ? dp[i][j + 1] : INT_MAX));
            }
        }
        return dp[0][0];
    }
};
```


