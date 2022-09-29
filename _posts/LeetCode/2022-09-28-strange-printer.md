---
layout: post
title: "Strange Printer Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 664. There is a strange printer with the following two special properties

---

<br />

## Description

LeetCode Problem 664.

There is a strange printer with the following two special properties:
* The printer can only print a sequence of the same character each time.
* At each turn, the printer can print new characters starting from and ending at any place and will cover the original existing characters.

Given a string s, return the minimum number of turns the printer needed to print it.

Example 1:
```
Input: s = "aaabbb"
Output: 2
Explanation: Print "aaa" first and then print "bbb".
```

Example 2:
```
Input: s = "aba"
Output: 2
Explanation: Print "aaa" first and then print "b" from the second place of the string, which will cover the existing character 'a'.
```

Constraints:
* 1 <= s.length <= 100
* s consists of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
private:
    int f[100][100];

private:
    // f[i][j] represents the minumum turns to print the sequence from i to j.
    // The transition function is: 
    // f[i][j] = min(f[i][k] + f[k+1][j-1]) for each k where i<k<j and s[k]=s[j]
    // f[i][j] = f[i][j-1] + 1
    // And the border condition: f[i][j] = 0 where i>j
    int dfs(const std::string& s, int l, int r) {
        if (l > r) 
            return 0;
        if (f[l][r]) 
            return f[l][r];
        
        f[l][r] = dfs(s, l, r - 1) + 1;
        for (int i = l; i < r; ++i) {
            if (s[i] == s[r]) {
                f[l][r] = std::min(f[l][r], dfs(s, l, i) + dfs(s, i + 1, r - 1));
            }
        }
        return f[l][r];
    }
    
public:
    int strangePrinter(std::string s) {
        memset(f, 0, sizeof(f));
        int len = (int)s.size();
        return dfs(s, 0, len - 1);
    }
};
```


