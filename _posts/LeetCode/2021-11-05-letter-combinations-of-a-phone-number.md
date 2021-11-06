---
layout: post
title:  "Letter Combinations of a Phone Number Problem"
categories: [ Algorithm ]
tags: [ Backtracking, Hash Table, String, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 17. Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. 
---

<br />

## Description

LeetCode Problem 17. 

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

```
2: abc
3: def
4: ghi
5: jkl
6: mno
7: pqrs
8: tuv
9: wxyz
```

 

Example 1:
```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

Example 2:
```
Input: digits = ""
Output: []
```

Example 3:
```
Input: digits = "2"
Output: ["a","b","c"]
```

Constraints:

* 0 <= digits.length <= 4
* digits[i] is a digit in the range ['2', '9'].

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<string> ans;
    vector<string> mapping = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    
    void dfs(string digits, string letters) {
        if (digits.size() == 0) {
            return;
        }
        int dig = digits[0] - '0';
        for (int i = 0; i < mapping[dig].size(); i ++) {
            letters += mapping[dig][i];
            if (digits.size() == 1)
                ans.push_back(letters);
            else
                dfs(digits.substr(1), letters);
            letters.erase(letters.end()-1);
        }
        return;
    }
    
    vector<string> letterCombinations(string digits) {
        dfs(digits, "");
        return ans;
    }
};
```
