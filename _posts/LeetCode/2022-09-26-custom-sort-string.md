---
layout: post
title: "Custom Sort String Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Sorting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 791. You are given two strings order and s. All the words of order are unique and were sorted in some custom order previously.

---

<br />

## Description

LeetCode Problem 791.

You are given two strings order and s. All the words of order are unique and were sorted in some custom order previously.

Permute the characters of s so that they match the order that order was sorted. More specifically, if a character x occurs before a character y in order, then x should occur before y in the permuted string.

Return any permutation of s that satisfies this property.

Example 1:
```
Input: order = "cba", s = "abcd"
Output: "cbad"
Explanation: 
"a", "b", "c" appear in order, so the order of "a", "b", "c" should be "c", "b", and "a". 
Since "d" does not appear in order, it can be at any position in the returned string. "dcba", "cdba", "cbda" are also valid outputs.
```

Example 2:
```
Input: order = "cbafg", s = "abcd"
Output: "cbad"
```

Constraints:
* 1 <= order.length <= 26
* 1 <= s.length <= 200
* order and s consist of lowercase English letters.
* All the characters of order are unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string customSortString(string S, string T) {
        unordered_map<char, int> dir;
        for (int i = 0; i < S.size(); i++) {
            dir[S[i]] = i + 1;
        }
        sort(T.begin(), T.end(),
             [&](char a, char b) { return dir[a] < dir[b]; });
        return T;
    }
};
```


