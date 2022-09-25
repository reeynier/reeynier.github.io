---
layout: post
title: "Target Sum Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming, Backtracking ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 494. You are given an integer array nums and an integer target.

---

<br />

## Description

LeetCode Problem 494.

You are given an integer array nums and an integer target.

You want to build an expression out of nums by adding one of the symbols '+' and '-' before each integer in nums and then concatenate all the integers.

* For example, if nums = [2, 1], you can add a '+' before 2 and a '-' before 1 and concatenate them to build the expression "+2-1".

Return the number of different expressions that you can build, which evaluates to target.

Example 1:
```
Input: nums = [1,1,1,1,1], target = 3
Output: 5
Explanation: There are 5 ways to assign symbols to make the sum of nums be target 3.
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3
```

Example 2:
```
Input: nums = [1], target = 1
Output: 1
```

Constraints:
* 1 <= nums.length <= 20
* 0 <= nums[i] <= 1000
* 0 <= sum(nums[i]) <= 1000
* -1000 <= target <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int S) {
        int sum = 0;
        for (auto n : nums) sum += n;
        if ((sum + S) % 2 == 1 || S > sum || S < -sum) return 0;
        int newS = (sum + S) / 2;
        vector<int> dp(newS + 1, 0);
        dp[0] = 1;
        for (int i = 0; i < nums.size(); ++i) {
            for (int j = newS; j >= nums[i]; --j) {
                dp[j] += dp[j - nums[i]];
            }
        }
        return dp[newS];
    }
};
```


