---
layout: post
title: "Satisfiability Of Equality Equations Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, String, Union Find, Graph ]
similar: [ Union Find ]
featured: false
hidden: false
excerpt: LeetCode 990. You are given an array of strings equations that represent relationships between variables where each string equations[i] 

---

<br />

## Description

LeetCode Problem 990.

You are given an array of strings equations that represent relationships between variables where each string equations[i] is of length 4 and takes one of two different forms: "x_i==y_i" or "x_i!=y_i".Here, x_i and y_i are lowercase letters (not necessarily different) that represent one-letter variable names.

Return true if it is possible to assign integers to variable names so as to satisfy all the given equations, or false otherwise.

Example 1:
```
Input: equations = ["a==b","b!=a"]
Output: false
Explanation: If we assign say, a = 1 and b = 1, then the first equation is satisfied, but not the second.
There is no way to assign the variables to satisfy both equations.
```

Example 2:
```
Input: equations = ["b==a","a==b"]
Output: true
Explanation: We could assign a = 1 and b = 1 to satisfy both equations.
```

Example 3:
```
Input: equations = ["a==b","b==c","a==c"]
Output: true
```

Example 4:
```
Input: equations = ["a==b","b!=c","c==a"]
Output: false
```

Example 5:
```
Input: equations = ["c==c","b==d","x!=z"]
Output: true
```

Constraints:
* 1 <= equations.length <= 500
* equations[i].length == 4
* equations[i][0] is a lowercase letter.
* equations[i][1] is either '=' or '!'.
* equations[i][2] is '='.
* equations[i][3] is a lowercase letter.

<br />

## Sample C++ Code using Union Find


```c
class Solution {
public:
    int _find(int p, vector<int>& nums) {
        while (p != nums[p])
            p = nums[p];
        return p;
    }
    void _union(int i, int j, vector<int>& nums) {
        int r1 = _find(i, nums);
        int r2 = _find(j, nums);
        if (r1 < r2)
            nums[r2] = r1;
        else
            nums[r1] = r2;
    }
    
    bool equationsPossible(vector<string>& equations) {
        vector<int> equal(26);
        for (int i = 0; i < 26; i ++) equal[i] = i;
        
        for (int i = 0; i < equations.size(); i ++) {
            if (equations[i][1] == '=') {
                _union(equations[i][0]-'a', equations[i][3]-'a', equal);
            }
        }
        
        for (int i = 0; i < equations.size(); i ++) {
            if (equations[i][1] == '!') {
                int left = equations[i][0] - 'a';
                int right = equations[i][3] - 'a';
                left = _find(left, equal);
                right = _find(right, equal);
                if (left == right)
                    return false;
            }
        }
        return true;
    }
};
```


