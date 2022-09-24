---
layout: post
title: "Ones And Zeroes Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, String, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 474. You are given an array of binary strings strs and two integers m and n.

---

<br />

## Description

LeetCode Problem 474.

You are given an array of binary strings strs and two integers m and n.

Return the size of the largest subset of strs such that there are at most m 0's and n 1's in the subset.

A set x is a subset of a set y if all elements of x are also elements of y.

Example 1:
```
Input: strs = ["10","0001","111001","1","0"], m = 5, n = 3
Output: 4
Explanation: The largest subset with at most 5 0's and 3 1's is {"10", "0001", "1", "0"}, so the answer is 4.
Other valid but smaller subsets include {"0001", "1"} and {"10", "1", "0"}.
{"111001"} is an invalid subset because it contains 4 1's, greater than the maximum of 3.
```

Example 2:
```
Input: strs = ["10","0","1"], m = 1, n = 1
Output: 2
Explanation: The largest subset is {"0", "1"}, so the answer is 2.
```

Constraints:
* 1 <= strs.length <= 600
* 1 <= strs[i].length <= 100
* strs[i] consists only of digits '0' and '1'.
* 1 <= m, n <= 100

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findMaxForm(vector<string>& strs, int m, int n) {
        vector<vector<int>> memo(m+1, vector<int>(n+1, 0));
        int numZeroes, numOnes;

        for (auto &s : strs) {
            numZeroes = numOnes = 0;
            // count number of zeroes and ones in current string
            for (auto c : s) {
                if (c == '0')
                    numZeroes++;
                else if (c == '1')
                    numOnes++;
            }

            // memo[i][j] = the max number of strings that can be formed with i 0's and j 1's
            // from the first few strings up to the current string s
            // Catch: have to go from bottom right to top left
            // Why? If a cell in the memo is updated(because s is selected),
            // we should be adding 1 to memo[i][j] from the previous iteration (when we were not considering s)
            // If we go from top left to bottom right, we would be using results from this iteration => overcounting
            for (int i = m; i >= numZeroes; i--) {
                for (int j = n; j >= numOnes; j--) {
                    memo[i][j] = max(memo[i][j], memo[i - numZeroes][j - numOnes] + 1);
                }
            }
        }
        return memo[m][n];
    }
};
```


