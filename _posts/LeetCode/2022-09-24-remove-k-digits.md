---
layout: post
title: "Remove K Digits Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Stack, Greedy, Monotonic Stack ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 402. Given string num representing a non-negative integer num, and an integer k, return the smallest possible integer after removing k digits from num.

---

<br />

## Description

LeetCode Problem 402.

Given string num representing a non-negative integer num, and an integer k, return the smallest possible integer after removing k digits from num.

Example 1:
```
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
```

Example 2:
```
Input: num = "10200", k = 1
Output: "200"
Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
```

Example 3:
```
Input: num = "10", k = 2
Output: "0"
Explanation: Remove all the digits from the number and it is left with nothing which is 0.
```

Constraints:
* 1 <= k <= num.length <= 10^5
* num consists of only digits.
* num does not have any leading zeros except for the zero itself.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string removeKdigits(string num, int k) {
        // treat ans as a stack in below for loop
        string ans = "";                                         

        for (char c : num) {
           while (ans.length() && ans.back() > c && k) {
               // make sure digits in ans are in ascending order
               ans.pop_back();                                  
               // remove one char
               k--;                                             
           }
           if (ans.length() || c != '0') 
               // can't have leading '0'
               ans.push_back(c);   
        }

        while (ans.length() && k--) 
           // make sure remove k digits in total
           ans.pop_back();           

        return ans.empty() ? "0" : ans;
    }
};
```


