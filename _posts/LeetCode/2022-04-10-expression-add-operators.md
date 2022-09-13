---
layout: post
title: "Expression Add Operators Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, String, Backtracking ]
similar: [ Backtracking ]
featured: false
hidden: false
excerpt: LeetCode 282. Given a string num that contains only digits and an integer target, return all possibilities to insert the binary operators '+', '-', and/or '\*' between the digits of num so that the resultant expression evaluates to the target value.
---

<br />

## Description

LeetCode Problem 282.

Given a string num that contains only digits and an integer target, return all possibilities to insert the binary operators '+', '-', and/or '\*' between the digits of num so that the resultant expression evaluates to the target value.

Note that operands in the returned expressions should not contain leading zeros.

Example 1:
```
Input: num = "123", target = 6
Output: ["1*2*3","1+2+3"]
Explanation: Both "1*2*3" and "1+2+3" evaluate to 6.
```

Example 2:
```
Input: num = "232", target = 8
Output: ["2*3+2","2+3*2"]
Explanation: Both "2*3+2" and "2+3*2" evaluate to 8.
```

Example 3:
```
Input: num = "105", target = 5
Output: ["1*0+5","10-5"]
Explanation: Both "1*0+5" and "10-5" evaluate to 5.
Note that "1-05" is not a valid expression because the 5 has a leading zero.
```

Example 4:
```
Input: num = "00", target = 0
Output: ["0*0","0+0","0-0"]
Explanation: "0*0", "0+0", and "0-0" all evaluate to 0.
Note that "00" is not a valid expression because the 0 has a leading zero.
```

Example 5:
```
Input: num = "3456237490", target = 9191
Output: []
Explanation: There are no expressions that can be created from "3456237490" to evaluate to 9191.
```

Constraints:
* 1 <= num.length <= 10
* num consists of only digits.
* -2^31 <= target <= 2^31 - 1

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<string> ans;
    string s;
    int target;
    vector<string> addOperators(string s, int target) {
        this->s = s;
        this->target = target;
        backtrack( 0, "", 0, 0);
        return ans;
    }
    void backtrack(int i, const string& path, long resSoFar, long prevNum) {
        if (i == s.length()) {
            if (resSoFar == target) ans.push_back(path);
            return;
        }
        string numStr;
        long num = 0;
        for (int j = i; j < s.length(); j++) {
            if (j > i && s[i] == '0') break; // Skip leading zero number
            numStr += s[j];
            num = num * 10 + s[j] - '0';
            if (i == 0) {
                backtrack(j + 1, path + numStr, num, num); // First num, pick it without adding any operator!
            } else {
                backtrack(j + 1, path + "+" + numStr, resSoFar + num, num);
                backtrack(j + 1, path + "-" + numStr, resSoFar - num, -num);
                backtrack(j + 1, path + "*" + numStr, resSoFar - prevNum + prevNum * num, prevNum * num); // Can imagine with example: 1-2*3
            }
        }
    }
};
```


