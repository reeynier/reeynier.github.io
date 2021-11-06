---
layout: post
title:  "Longest Common Prefix Problem"
categories: [ Data Structure ]
tags: [String, Leetcode ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 14. Write a function to find the longest common prefix string amongst an array of strings.
---

<br />

## Description

LeetCode Problem 14. 

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

 

Example 1:
```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```

Example 2:
```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

Constraints:

* 1 <= strs.length <= 200
* 0 <= strs[i].length <= 200
* strs[i] consists of only lower-case English letters.


<br />

## Sample C++ Code


```c
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if (strs.size() == 0)
            return "";
        string prefix = strs[0];
        int p = strs[0].size();
        int i, j;
        for (i = 0; i < strs.size(); i ++) {
            for (j = 0; j < p; j ++) {
                if (prefix[j] != strs[i][j])
                    break;
            }
            p = j;
            prefix = prefix.substr(0, p);
        }
        return prefix;
    }
};
```
