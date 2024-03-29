---
layout: post
title: "Numbers With Same Consecutive Differences Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Backtracking, Breadth-First Search ]
similar: [ Breadth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 967. Return all non-negative integers of length n such that the absolute difference between every two consecutive digits is k.

---

<br />

## Description

LeetCode Problem 967.

Return all non-negative integers of length n such that the absolute difference between every two consecutive digits is k.

Note that every number in the answer must not have leading zeros. For example, 01 has one leading zero and is invalid.

You may return the answer in any order.

Example 1:
```
Input: n = 3, k = 7
Output: [181,292,707,818,929]
Explanation: Note that 070 is not a valid number, because it has leading zeroes.
```

Example 2:
```
Input: n = 2, k = 1
Output: [10,12,21,23,32,34,43,45,54,56,65,67,76,78,87,89,98]
```

Example 3:
```
Input: n = 2, k = 0
Output: [11,22,33,44,55,66,77,88,99]
```

Example 4:
```
Input: n = 2, k = 2
Output: [13,20,24,31,35,42,46,53,57,64,68,75,79,86,97]
```

Constraints:
* 2 <= n <= 9
* 0 <= k <= 9

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> numsSameConsecDiff(int n, int k) {     
        queue<int> q;
        for (int i = 1; i < 10; i++) {
            q.push(i);
        }
        for (int i = 1; i < n; i++) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                int num = q.front(); q.pop();
                int unit = num % 10;
                if (unit + k < 10)
                    q.push(num * 10 + unit + k);
                if (unit-k >= 0 && k != 0)
                    q.push(num * 10 + unit - k);
            }
        }
        vector<int> ans;
        if (n == 1) 
            ans.push_back(0);
        while (!q.empty()) {
            ans.push_back(q.front());
            q.pop();
        }
        return ans;
    }
};
```


