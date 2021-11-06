---
layout: post
title:  "Roman to Integer Problem"
categories: [ Algorithm ]
tags: [ Math, Hash Table, String, Leetcode ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 13. Given a roman numeral, convert it to an integer.
---

<br />

## Description

LeetCode Problem 13. 

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.
```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, 2 is written as II in Roman numeral, just two one's added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

* I can be placed before V (5) and X (10) to make 4 and 9. 
* X can be placed before L (50) and C (100) to make 40 and 90. 
* C can be placed before D (500) and M (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer.
 

Example 1:
```
Input: s = "III"
Output: 3
```

Example 2:
```
Input: s = "IV"
Output: 4
```

Example 3:
```
Input: s = "IX"
Output: 9
```

Example 4:
```
Input: s = "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```

Example 5:
```
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

Constraints:

* 1 <= s.length <= 15
* s contains only the characters ('I', 'V', 'X', 'L', 'C', 'D', 'M').
* It is guaranteed that s is a valid roman numeral in the range [1, 3999].


<br />

## Sample C++ Code


```c
class Solution {
public:
    int romanToInt(string s) {
        unordered_map<char, int> ht;
        ht['I'] = 1;
        ht['V'] = 5;
        ht['X'] = 10;
        ht['L'] = 50;
        ht['C'] = 100;
        ht['D'] = 500;
        ht['M'] = 1000;
        
        stack<int> st;
        st.push(ht[s[0]]);
        int ans = ht[s[0]];
        for (int i = 1; i < s.size(); i ++) {
            ans += ht[s[i]];
            if (s[i] == 'V' || s[i] == 'X') {
                while (!st.empty() && st.top() == 1) {
                    ans -= 2;
                    st.pop();
                }
            } else if (s[i] == 'L' || s[i] == 'C') {
                while (!st.empty() && st.top() == 10) {
                    ans -= 20;
                    st.pop();
                }
            } else if (s[i] == 'D' || s[i] == 'M') {
                while (!st.empty() && st.top() == 100) {
                    ans -= 200;
                    st.pop();
                }
            }
            st.push(ht[s[i]]);
        }
        
        return ans;
    }
};
```
