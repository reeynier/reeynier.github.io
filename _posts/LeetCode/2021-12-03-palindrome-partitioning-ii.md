---
layout: post
title: "Palindrome Partitioning II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 132. Given a string s, partition s such that every substring of the partition is a palindrome.

---

<br />

## Description

LeetCode Problem 132.

Given a string s, partition s such that every substring of the partition is a palindrome.

Return the minimum cuts needed for a palindrome partitioning of s.

Example 1:
```
Input: s = "aab"
Output: 1
Explanation: The palindrome partitioning ["aa","b"] could be produced using 1 cut.
```

Example 2:
```
Input: s = "a"
Output: 0
```

Example 3:
```
Input: s = "ab"
Output: 1
```

Constraints:
* 1 <= s.length <= 2000
* s consists of lower-case English letters only.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int minCut(string s) {
        int len = s.size();
        vector<vector<int>> dp(len, vector<int>(len, 1));
        
        for (int i = 0; i < len; i ++) {
            for (int j = i-1; j >= 0; j --) {
                if (s[i] != s[j]) 
                    dp[j][i] = 0;
                if (!dp[j+1][i-1])
                    dp[j][i] = 0;
            }
        }
        
        vector<int> cut(len, INT_MAX);
        for (int i = 0; i < len; i ++) {
            for (int j = 0; j < i+1; j ++) {
                if (dp[j][i]) {
                    if (j != 0)
                        cut[i] = min(cut[i], cut[j-1]+1);
                    else
                        cut[i] = min(cut[i], 0);
                }
            }
        }
        
        return cut[len-1];
    }
};
```


