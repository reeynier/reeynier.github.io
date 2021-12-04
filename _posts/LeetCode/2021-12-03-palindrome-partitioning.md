---
layout: post
title: "Palindrome Partitioning Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Dynamic Programming, Backtracking ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 131. Given a string s, partition s such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of s.

---

<br />

## Description

LeetCode Problem 131.

Given a string s, partition s such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of s.

A palindrome string is a string that reads the same backward as forward.

Example 1:
```
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
```

Example 2:
```
Input: s = "a"
Output: [["a"]]
```

Constraints:
* 1 <= s.length <= 16
* s contains only lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    void dfs(vector<vector<int>>& dp, vector<vector<string>>& ans, 
            vector<string>& line, int idx, string& s) {
        if (idx >= s.size()) {
            ans.push_back(line);
            return;
        }
        for (int i = idx; i < s.size(); i ++) {
            if (dp[idx][i]) {
                string t = s.substr(idx, i - idx + 1);
                line.push_back(t);
                dfs(dp, ans, line, i+1, s);
                line.pop_back();
            }
        }
        return;
    }
    vector<vector<string>> partition(string s) {
        int len = s.size();
        vector<vector<int>> dp(len, vector<int>(len, 1));
        
        for (int i = 0; i < len; i ++) {
            for (int j = i-1; j >= 0; j --) {
                if (s[j] != s[i])
                    dp[j][i] = 0;
                if (!dp[j+1][i-1])
                    dp[j][i] = 0;
            }
        }
        
        vector<vector<string>> ans;
        vector<string> line;
        dfs(dp, ans, line, 0, s);
        return ans;
    }
};
```


