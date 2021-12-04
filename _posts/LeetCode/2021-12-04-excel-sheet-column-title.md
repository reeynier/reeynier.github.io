---
layout: post
title: "Excel Sheet Column Title Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, String ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 168. Given an integer columnNumber, return its corresponding column title as it appears in an Excel sheet.

---

<br />

## Description

LeetCode Problem 168.

Given an integer columnNumber, return its corresponding column title as it appears in an Excel sheet.

For example:
```
A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28 
...
```

Example 1:
```
Input: columnNumber = 1
Output: "A"
```

Example 2:
```
Input: columnNumber = 28
Output: "AB"
```

Example 3:
```
Input: columnNumber = 701
Output: "ZY"
```

Example 4:
```
Input: columnNumber = 2147483647
Output: "FXSHRXW"
```

Constraints:
* 1 <= columnNumber <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    string convertToTitle(int n) {
        string ans;
        int p;
        while (n > 0) {
            p = n % 26;
            n = n / 26;
            if (p == 0) {
                p = 26;
                n --;
            }
            ans += 'A' + p - 1;
        }
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```


