---
layout: post
title: "Valid Permutations For DI Sequence Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 903. You are given a string s of length n where s[i] is either

---

<br />

## Description

LeetCode Problem 903.

You are given a string s of length n where s[i] is either:
* 'D' means decreasing, or
* 'I' means increasing.

A permutation perm of n + 1 integers of all the integers in the range [0, n] is called a valid permutation if for all valid i:
* If s[i] == 'D', then perm[i] > perm[i + 1], and
* If s[i] == 'I', then perm[i] < perm[i + 1].

Return the number of valid permutations perm. Since the answer may be large, return it modulo 10^9 + 7.

Example 1:
```
Input: s = "DID"
Output: 5
Explanation: The 5 valid permutations of (0, 1, 2, 3) are:
(1, 0, 3, 2)
(2, 0, 3, 1)
(2, 1, 3, 0)
(3, 0, 2, 1)
(3, 1, 2, 0)
```

Example 2:
```
Input: s = "D"
Output: 1
```

Constraints:
* n == s.length
* 1 <= n <= 200
* s[i] is either 'I' or 'D'.

<br />

## Sample C++ Code


```c
class Solution {
public:
    // dp[i]:the total possible permutations count of first i+1 digits
    // denote j as the i+1th digit is the j+1th smallest number in the rest not-yet-select digits.
    // dp[i][j]: the total possible numbers of first i+1 digits, 
    // where i+1th digit is the jth smallest number in the rest not-yet-select digits.
    // if we add a digit k as the first ith digit, and S[i]=='I', 
    // we know that we can only add those digit which bigger than k as the first i+1th digit, 
    // i.e., dp[i][j] can only form those dp[i][w], where w>=j.
    // example: S="DID", and we choose digit 2 as the first digit, 
    // then when choosing the second digit, we can only choose those bigger than 2 
    // because we need "increase". So we choose 3 and 4, noticing that 3 and 4 
    // is the 2nd smallest and 3rd smallest in the rest non-select-yet digit [1,3,4].
    int numPermsDISequence(string S) {
        int n = S.length(), mod = 1e9 + 7;
        vector<vector<int>> dp(n + 1, vector<int>(n + 1));
        for (int j = 0; j <= n; j++) dp[0][j] = 1;
        for (int i = 0; i < n; i++)
            if (S[i] == 'I')
                for (int j = 0, cur = 0; j < n - i; j++)
                    dp[i + 1][j] = cur = (cur + dp[i][j]) % mod;
            else
                for (int j = n - i - 1, cur = 0; j >= 0; j--)
                    dp[i + 1][j] = cur = (cur + dp[i][j + 1]) % mod;
        
        return dp[n][0];
    }
};
```


