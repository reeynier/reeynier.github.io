---
layout: post
title: "Length Of Longest Fibonacci Subsequence Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Dynamic Programming ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 873. Given a strictly increasing array arr of positive integers forming a sequence, return the length of the longest Fibonacci-like subsequence of arr.

---

<br />

## Description

LeetCode Problem 873.

A sequence x_1, x_2, ..., x_n is Fibonacci-like if:
* n >= 3
* x_i + x_i+1 == x_i+2 for all i + 2 <= n

Given a strictly increasing array arr of positive integers forming a sequence, return the length of the longest Fibonacci-like subsequence of arr. If one does not exist, return 0.

A subsequence is derived from another sequence arr by deleting any number of elements (including none) from arr, without changing the order of the remaining elements. For example, [3, 5, 8] is a subsequence of [3, 4, 5, 6, 7, 8].

Example 1:
```
Input: arr = [1,2,3,4,5,6,7,8]
Output: 5
Explanation: The longest subsequence that is fibonacci-like: [1,2,3,5,8].
```

Example 2:
```
Input: arr = [1,3,7,11,12,14,18]
Output: 3
Explanation: The longest subsequence that is fibonacci-like: [1,11,12], [3,11,14] or [7,11,18].
```

Constraints:
* 3 <= arr.length <= 1000
* 1 <= arr[i] < arr[i + 1] <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    int lenLongestFibSubseq(vector<int>& a) {
        int n = a.size();
        // dp[i][j] stores the length of the fibonnaci sequence ending with i, j.
        vector<vector<int>> dp(n, vector<int>(n, 0));
        int maxi = 0;
        
        for (int i = 2; i < n; i++) {
            int l = 0, r = i - 1;

            // check if we can find a[l] + a[r] = a[i]
            while (l < r) {
                int sum = a[l] + a[r];
                if (sum > a[i]) 
                    r--;
                else if (sum < a[i]) 
                    l++;
                else {
                    // we found a fibonacci sequence ending with indices r and i.
                    // we update dp[r][i] to dp[l][r] + 1.
                    dp[r][i] = dp[l][r] + 1;
                    maxi = max(maxi, dp[r][i]);
                    l++;
                    r--;
                }
            }
        }
        
        return maxi == 0 ? 0 : maxi + 2;
    }
};
```


