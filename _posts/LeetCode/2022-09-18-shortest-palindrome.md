---
layout: post
title: "Shortest Palindrome Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Rolling Hash, String Matching, Hash Function ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 214. You are given a string s. You can convert s to a palindrome by adding characters in front of it.

---

<br />

## Description

LeetCode Problem 214.

You are given a string s. You can convert s to a palindrome by adding characters in front of it.

Return the shortest palindrome you can find by performing this transformation.

Example 1:
```
Input: s = "aacecaaa"
Output: "aaacecaaa"
```

Example 2:
```
Input: s = "abcd"
Output: "dcbabcd"
```

Constraints:
* 0 <= s.length <= 5 * 10^4
* s consists of lowercase English letters only.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string shortestPalindrome(string s) {
        int n = s.size();
        int i = 0;
        for (int j = n - 1; j >= 0; j--) {
            if (s[i] == s[j])
                i++;
        }
        if (i == n) {
            return s;
        }
        string remain_rev = s.substr(i, n);
        reverse(remain_rev.begin(), remain_rev.end());
        return remain_rev + shortestPalindrome(s.substr(0, i)) + s.substr(i);
    }
};
```


