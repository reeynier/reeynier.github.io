---
layout: post
title: "Strong Password Checker Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Greedy, Heap ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 420. A password is considered strong if the below conditions are all met

---

<br />

## Description

LeetCode Problem 420.

A password is considered strong if the below conditions are all met:
* It has at least 6 characters and at most 20 characters.
* It contains at least one lowercase letter, at least one uppercase letter, and at least one digit.
* It doesnot contain three repeating characters in a row (i.e.,"...aaa..." is weak, but "...aa...a..." is strong, assuming other conditions are met).

Given a string password, return the minimum number of steps required to make password strong. if password is already strong, return 0.

In one step, you can:
* Insert one character to password,
* Delete one character from password, or
* Replaceone character of password with another character.

Example 1:
```
Input: password = "a"
Output: 5
```

Example 2:
```
Input: password = "aA1"
Output: 3
```

Example 3:
```
Input: password = "1337C0d3"
Output: 0
```

Constraints:
* 1 <= password.length <= 50
* password consists of letters, digits, dot'.' or exclamation mark '!'.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isLower(char c) { return c >= 'a' && c <= 'z'; }
    bool isUpper(char c) { return c >= 'A' && c <= 'Z'; }
    bool isNumber(char c) { return c >= '0' && c <= '9'; }
    
    int strongPasswordChecker(string password) {
        int n = password.size();
        if (!n) return 6;                    
        int repeat = 1, replace = 0, remove = 0, add = 0;
        char cur = password[0];
        int lower = isLower(cur), upper = isUpper(cur), number = isNumber(cur);
        vector<int> repeatVec;
        for (int i = 1; i < n; ++i) {
            lower += isLower(password[i]);
            upper += isUpper(password[i]);
            number += isNumber(password[i]);
            if (password[i] == cur) ++repeat;
            if (password[i] != cur || i == n-1) {
                replace += repeat/3;
                add += (repeat-1)/2;
                remove += max(0, repeat-2);
                if (repeat > 2) 
                    repeatVec.push_back(repeat);
                repeat = 1;
                cur = password[i];
            }
        } 
        int miss = 0;
        if (!lower) ++miss;
        if (!upper) ++miss;
        if (!number) ++miss;
        if (n < 6) return max(max(6 - n, miss), add);        
        if (n <= 20) return max(replace, miss);        
        int needRemove = n - 20;
        if (needRemove >= remove) 
            return needRemove + miss;
        else { 
            int R = needRemove, m = repeatVec.size();
            vector<vector<int>> dp(R+1, vector<int>(m+1, INT_MAX));
            dp[0][0] = 0;
            for (int j = 1; j <= m; ++j) 
                dp[0][j] = dp[0][j-1] + repeatVec[j-1]/3;            
            for (int r = 1; r <= R; ++r) 
                for (int j = 1; j <= m; ++j) 
                    for (int s = 0; s <= min(repeatVec[j-1]-2, r); ++s) 
                        if (dp[r-s][j-1] < INT_MAX) 
                            dp[r][j] = min(dp[r][j], dp[r-s][j-1] + (repeatVec[j-1]-s)/3);
            return needRemove + max(dp[R][m], miss);
        }
    }
};
```


