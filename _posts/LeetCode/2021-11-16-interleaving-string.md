---
layout: post
title:  "Interleaving String Problem"
categories: [ Algorithm ]
tags: [ String, Dynamic Programming, Leetcode ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 97. Given strings s1, s2, and s3, find whether s3 is formed by an interleaving of s1 and s2.
---

<br />

## Description

LeetCode Problem 97. 

Given strings s1, s2, and s3, find whether s3 is formed by an interleaving of s1 and s2.

An interleaving of two strings s and t is a configuration where they are divided into non-empty substrings such that:

* s = s1 + s2 + ... + sn
* t = t1 + t2 + ... + tm
* |n - m| <= 1
* The interleaving is s1 + t1 + s2 + t2 + s3 + t3 + ... or t1 + s1 + t2 + s2 + t3 + s3 + ...

Note: a + b is the concatenation of strings a and b.


Example 1:
```
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
Output: true
```

Example 2:
```
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"
Output: false
```

Example 3:
```
Input: s1 = "", s2 = "", s3 = ""
Output: true
```

Constraints:

* 0 <= s1.length, s2.length <= 100
* 0 <= s3.length <= 200
* s1, s2, and s3 consist of lowercase English letters.

<br />

## Sample C++ Code


```c
bool isInterleave(string s1, string s2, string s3) {
    if (s3.length() != s1.length() + s2.length())
        return false;
    
    bool table[s1.length()+1][s2.length()+1];
    
    for (int i=0; i<s1.length()+1; i++)
        for (int j=0; j< s2.length()+1; j++){
            if (i==0 && j==0)
                table[i][j] = true;
            else if (i == 0)
                table[i][j] = (table[i][j-1] && s2[j-1] == s3[i+j-1]);
            else if (j == 0)
                table[i][j] = (table[i-1][j] && s1[i-1] == s3[i+j-1]);
            else
                table[i][j] = (table[i-1][j] && s1[i-1] == s3[i+j-1]) || 
                        (table[i][j-1] && s2[j-1] == s3[i+j-1]);
        }
        
    return table[s1.length()][s2.length()];
}
```
