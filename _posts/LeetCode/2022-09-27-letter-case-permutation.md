---
layout: post
title: "Letter Case Permutation Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Backtracking, Bit Manipulation ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 784. Given a string s, we can transform every letter individually to be lowercase or uppercase to create another string.

---

<br />

## Description

LeetCode Problem 784.

Given a string s, we can transform every letter individually to be lowercase or uppercase to create another string.

Return a list of all possible strings we could create. You can return the outputin any order.

Example 1:
```
Input: s = "a1b2"
Output: ["a1b2","a1B2","A1b2","A1B2"]
```

Example 2:
```
Input: s = "3z4"
Output: ["3z4","3Z4"]
```

Example 3:
```
Input: s = "12345"
Output: ["12345"]
```

Example 4:
```
Input: s = "0"
Output: ["0"]
```

Constraints:
* s will be a string with length between 1 and 12.
* s will consist only of letters or digits.

<br />

## Sample C++ Code


```c
class Solution {
    void backtrack(string &s, int i, vector<string> &res) {
        if (i == s.size()) {
            res.push_back(s);
            return;
        }
        backtrack(s, i + 1, res);
        if (isalpha(s[i])) {
            // toggle case
            s[i] ^= (1 << 5);
            backtrack(s, i + 1, res);
        }
    }
public:
    vector<string> letterCasePermutation(string S) {
        vector<string> res;
        backtrack(S, 0, res);
        return res;
    }
};
```


