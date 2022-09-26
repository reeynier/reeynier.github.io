---
layout: post
title: "Student Attendance Record II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 552. An attendance record for a student can be represented as a string where each character signifies whether the student was absent, late, or present on that day. The record only contains the following three characters

---

<br />

## Description

LeetCode Problem 552.

An attendance record for a student can be represented as a string where each character signifies whether the student was absent, late, or present on that day. The record only contains the following three characters:
* 'A': Absent.
* 'L': Late.
* 'P': Present.

Any student is eligible for an attendance award if they meet both of the following criteria:
* The student was absent ('A') for strictly fewer than 2 days total.
* The student was never late ('L') for 3 or more consecutive days.

Given an integer n, return the number of possible attendance records of length n that make a student eligible for an attendance award. The answer may be very large, so return it modulo 10^9 + 7.

Example 1:
```
Input: n = 2
Output: 8
Explanation: There are 8 records with length 2 that are eligible for an award:
"PP", "AP", "PA", "LP", "PL", "AL", "LA", "LL"
Only "AA" is not eligible because there are 2 absences (there need to be fewer than 2).
```

Example 2:
```
Input: n = 1
Output: 3
```

Example 3:
```
Input: n = 10101
Output: 183236316
```

Constraints:
* 1 <= n <= 10^5

<br />

## Sample C++ Code


```c
class Solution {
public:
    long long int mod = 1e9 + 7;
    long long int dp[100001][2][3];
    
    int helper(int n, int absent, int late) { 
        if (late >= 3 || absent >= 2) 
            // not an eligible record condition 
            return 0; 
        if (n == 0) 
            // recurrence call till n == 0, i.e. we got an eligible record
            return 1; 
        
        //Memoization 
        if (dp[n][absent][late] != -1) 
        	return dp[n][absent][late];
        
        //Recurrence calls
        int p_selected = helper(n-1, absent, 0); // if we selected Present
        int a_selected = helper(n-1, absent + 1, 0); // if we selected Absent
        int l_selected = helper(n-1, absent, late + 1); // if we selected Late
        
        // Output = Sum of all three recurrence call outputs 
        return dp[n][absent][late] = (p_selected%mod + a_selected%mod + l_selected%mod ) % mod;
    }
    
    int checkRecord(int n) {
        //Initializing dp with -1
        memset(dp, -1, sizeof(dp));
        return helper(n, 0, 0);
    }
};
```


