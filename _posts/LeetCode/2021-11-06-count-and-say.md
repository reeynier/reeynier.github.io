---
layout: post
title:  "Count and Say Problem"
categories: [ Data Structure ]
tags: [ String, Leetcode ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 38. Write the code that will take a string and make this conversion given a number of rows.
---

<br />

## Description

LeetCode Problem 38. 

The count-and-say sequence is a sequence of digit strings defined by the recursive formula:

* countAndSay(1) = "1"
* countAndSay(n) is the way you would "say" the digit string from countAndSay(n-1), which is then converted into a different digit string.

To determine how you "say" a digit string, split it into the minimal number of groups so that each group is a contiguous section all of the same character. Then for each group, say the number of characters, then say the character. To convert the saying into a digit string, replace the counts with a number and concatenate every saying.

For example, the saying and conversion for digit string "3322251":
```
"3322251"
two 3's, three 2's, one 5, and on2 1
2 3 + 3 2 + 1 5 + 1 1
"23321511"
```

Given a positive integer n, return the nth term of the count-and-say sequence.

 

Example 1:
```
Input: n = 1
Output: "1"
Explanation: This is the base case.
```

Example 2:
```
Input: n = 4
Output: "1211"
Explanation:
countAndSay(1) = "1"
countAndSay(2) = say "1" = one 1 = "11"
countAndSay(3) = say "11" = two 1's = "21"
countAndSay(4) = say "21" = one 2 + one 1 = "12" + "11" = "1211"
```

Constraints:

* 1 <= n <= 30



<br />

## Sample C++ Code


```c
string countAndSay(int n) {
    if (n == 0) return "";
    string res = "1";
    while (--n) {
        string cur = "";
        for (int i = 0; i < res.size(); i++) {
            int count = 1;
             while ((i + 1 < res.size()) && (res[i] == res[i + 1])){
                count++;    
                i++;
            }
            cur += to_string(count) + res[i];
        }
        res = cur;
    }
    return res;
}
```
