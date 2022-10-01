---
layout: post
title: "Count Unique Characters Of All Substrings Of A Given String Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Dynamic Programming ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 828. Let's define a function countUniqueChars(s) that returns the number of unique characters on s.

---

<br />

## Description

LeetCode Problem 828.

Let's define a function countUniqueChars(s) that returns the number of unique characters on s.
* For example if s = "LEETCODE" then "L", "T", "C", "O", "D" are the unique characters since they appear only once in s, therefore countUniqueChars(s) = 5.

Given a string s, return the sum of countUniqueChars(t) where t is a substring of s.

Notice that some substrings can be repeated so in this case you have to count the repeated ones too.

Example 1:
```
Input: s = "ABC"
Output: 10
Explanation: All possible substrings are: "A","B","C","AB","BC" and "ABC".
Evey substring is composed with only unique letters.
Sum of lengths of all substring is 1 + 1 + 1 + 2 + 2 + 3 = 10
```

Example 2:
```
Input: s = "ABA"
Output: 8
Explanation: The same as example 1, except countUniqueChars("ABA") = 1.
```

Example 3:
```
Input: s = "LEETCODE"
Output: 92
```

Constraints:
* 1 <= s.length <= 10^5
* s consists of uppercase English letters only.

<br />

## Sample C++ Code


```c
class Solution {
public:
    // Occurences: at first 0, so we'll use 1-based indexing
    int cur[26], prev[26]; 
    
    int uniqueLetterString(string& s) {
        int i, n = s.size(); 
        long long total = 0LL; 
        char ch;

        // prev - cur - next trio of indexes of char ch
        // in how many substrings ch with position cur will be unique?
        // potential starting points are [prev + 1, cur], ending points are[cur, next - 1]
        // so each time total += (cur - prev) * (next - cur)
        for (i = 1; i <= n; i++) {
            ch = s[i - 1] - 'A';
            total += (cur[ch] - prev[ch]) * (i - cur[ch]);
            prev[ch] = cur[ch];
            cur[ch] = i;
        }
        
        // Haven't counted last occurences yet, so IMAGINE each letter pushed-back to string s
        for (ch = 0; ch < 26; ch++) 
            total += (cur[ch] - prev[ch]) * (n + 1 - cur[ch]);
        
        return total;
    }
};
```


