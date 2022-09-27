---
layout: post
title: "Repeated String Match Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 686. Given two string s a and b, return the minimum number of times you should repeat string a so that string b is a substring of it. If it is impossible for b​​​​​​ to be a substring ofa after repeating it, return -1.

---

<br />

## Description

LeetCode Problem 686.

Given two strings a and b, return the minimum number of times you should repeat string a so that string b is a substring of it. If it is impossible for b​​​​​​ to be a substring of a after repeating it, return -1.

Notice: string "abc" repeated 0 times is "", repeated 1 time is "abc" and repeated 2 times is "abcabc".

Example 1:
```
Input: a = "abcd", b = "cdabcdab"
Output: 3
Explanation: We return 3 because by repeating a three times "abcdabcdabcd", b is a substring of it.
```

Example 2:
```
Input: a = "a", b = "aa"
Output: 2
```

Example 3:
```
Input: a = "a", b = "a"
Output: 1
```

Example 4:
```
Input: a = "abc", b = "wxyz"
Output: -1
```

Constraints:
* 1 <= a.length <= 10^4
* 1 <= b.length <= 10^4
* aandbconsist of lower-case English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int repeatedStringMatch(string A, string B) {
        int len_a = A.size();
        int len_b = B.size();
        int n = len_b / len_a + 2; // 1 is for the round up, 1 is for 1 more repeat
        int i;
        string r_A = A;
        for (i = 1; i <= n; i ++) {
            if (r_A.find(B) != string::npos) {
                return i;
            } else {
                r_A += A;
            }
        }
        return -1;
    }
};
```


