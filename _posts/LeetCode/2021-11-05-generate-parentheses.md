---
layout: post
title:  "Generate Parentheses Problem"
categories: [ Data Structure ]
tags: [ Dynamic Programming, Backtracking, String, Leetcode ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 22. Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.
---

<br />

## Description

LeetCode Problem 22. 

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

 

Example 1:
```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

Example 2:
```
Input: n = 1
Output: ["()"]
```

Constraints:

* 1 <= n <= 8


<br />

## Sample C++ Code


```c
class Solution {
public:
    string paren = "()";
    vector<string> ans;
    int N;
    
    
    void dfs(string& s, int left, int right) {
        if (s.size() == N*2) {
            ans.push_back(s);
            return;
        }
        
            if (left < N) {
                s += '(';
                dfs(s, left+1, right);
                s.pop_back();
            }
            if (right < left) {
                s += ')';
                dfs(s, left, right+1);
                s.pop_back();
            }

    }
    
    vector<string> generateParenthesis(int n) {
        N = n;
        string s;
        dfs(s, 0, 0);
        
        return ans;
    }
};
```
