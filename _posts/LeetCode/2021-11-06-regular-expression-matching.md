---
layout: post
title:  "Regular Expression Matching Problem"
categories: [ Algorithm ]
tags: [ String, Dynamic Programming, Recursion, Leetcode ]
similar: [ Recursion ]
featured: false
hidden: false
excerpt: LeetCode 10. Given an input string s and a pattern p, implement regular expression matching.
---

<br />

## Description

LeetCode Problem 10. 

Given an input string s and a pattern p, implement regular expression matching with support for '.' and '*' where:

* '.' Matches any single character.​​​​
* '*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).
 

Example 1:
```
Input: s = "aa", p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".
```

Example 2:
```
Input: s = "aa", p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".
```

Example 3:
```
Input: s = "ab", p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
```

Example 4:
```
Input: s = "aab", p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab".
```

Example 5:
```
Input: s = "mississippi", p = "mis*is*p*."
Output: false
```
 

Constraints:

* 1 <= s.length <= 20
* 1 <= p.length <= 30
* s contains only lowercase English letters.
* p contains only lowercase English letters, '.', and '*'.
* It is guaranteed for each appearance of the character '*', there will be a previous valid character to match.


<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isMatch(string s, string p) {
       int n = s.length();
       int m = p.length(); 
       vector<vector<int>> dp(n+1, vector<int>(m+1,0));
       dp[0][0]=1; 
       
       for(int i=1; i<=m; i++){
           if(p[i-1]=='*'){
               dp[0][i]=dp[0][i-2];
           }
       } 
        
       for(int i=1; i<=n; i++){
           for(int j=1; j<=m; j++){
               
               if(s[i-1]==p[j-1] || p[j-1]=='.'){
                   dp[i][j]=dp[i-1][j-1];
               }
               else if(p[j-1]=='*'){
                   dp[i][j]=(dp[i][j-2] || (dp[i-1][j] && (p[j-2]=='.' || p[j-2]==s[i-1])));
               }
               
           }
       }
        
       return dp[n][m]; 
    }
};
```
