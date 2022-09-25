---
layout: post
title: "Reverse Words In A String III Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Two Pointers, String ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 557. Given a string s, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

---

<br />

## Description

LeetCode Problem 557.

Given a string s, reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

Example 1:
```
Input: s = "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```

Example 2:
```
Input: s = "God Ding"
Output: "doG gniD"
```

Constraints:
* 1 <= s.length <= 5 * 10^4
* s contains printable ASCII characters.
* s does not contain any leading or trailing spaces.
* There is at least one word in s.
* All the words in s are separated by a single space.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string reverseWords(string& s) {
        int i = 0;
        for (int j = 0; j < s.size(); ++j) {
            if (s[j] == ' ') {
                reverse(s.begin() + i, s.begin() + j);
                i = j + 1;
            }
        }
        reverse(s.begin() + i, s.end());
        return s;
    }
};
```


