---
layout: post
title: "Remove Invalid Parentheses Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String, Backtracking, Breadth-First Search ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 301. Given a string s that contains parentheses and letters, remove the minimum number of invalid parentheses to make the input string valid.

---

<br />

## Description

LeetCode Problem 301.

Given a string s that contains parentheses and letters, remove the minimum number of invalid parentheses to make the input string valid.

Return all the possible results. You may return the answer in any order.

Example 1:
```
Input: s = "()())()"
Output: ["(())()","()()()"]
```

Example 2:
```
Input: s = "(a)())()"
Output: ["(a())()","(a)()()"]
```

Example 3:
```
Input: s = ")("
Output: [""]
```

Constraints:
* 1 <= s.length <= 25
* s consists of lowercase English letters and parentheses '(' and ')'.
* There will be at most 20 parentheses in s.

<br />

## Sample C++ Code


```c
class Solution {
public:
    set<string> paren;
    
    bool checkValid(string s) {
        stack<char> st;
        for (int i = 0; i < s.size(); i ++) {
            if (s[i] == '(')
                st.push(s[i]);
            else if (s[i] == ')') {
                if (st.empty())
                    return false;
                st.pop();
            } else {
                continue;
            }
        }
        if (st.empty())
            return true;
        else
            return false;
    }
    
    void dfs(string s, int idx, int l) {
        
        if (s.size() == l) {
            bool flag = checkValid(s);
            if (flag)
                paren.insert(s);
            return;
        }
        if (idx > l || s.size() < l)
            return;
        
        if (s[idx] != '(' && s[idx] != ')')
            dfs(s, idx+1, l);
        else {
            dfs(s, idx+1, l);

            string ns = s.substr(0, idx)+s.substr(idx+1, s.size()-idx-1);
            dfs(ns, idx, l);
        }
        
    }
    
    vector<string> removeInvalidParentheses(string s) {
        stack<char> st;
        for (int i = 0; i < s.size(); i ++) {
            if (s[i] == '(')
                st.push(s[i]);
            else if (s[i] == ')') {
                if (!st.empty() && st.top() == '(')
                    st.pop();
                else
                    st.push(s[i]);
            } 
        }
        
        int l = s.size() - st.size();

        dfs(s, 0, l);
        
        vector<string> ans;
        for (auto x : paren)
            ans.push_back(x);
        return ans;
    }
};
```


