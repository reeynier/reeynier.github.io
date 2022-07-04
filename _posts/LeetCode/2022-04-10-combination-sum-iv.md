---
layout: post
title: "Combination Sum IV Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 377. Given an array of distinct integers nums and a target integer target, return the number of possible combinations that add up totarget.

---

<br />

## Description

LeetCode Problem 377.

Given an array of distinct integers nums and a target integer target, return the number of possible combinations that add up totarget.

The answer is guaranteed to fit in a 32-bit integer.

Example 1:
```
Input: nums = [1,2,3], target = 4
Output: 7
Explanation:
The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)
Note that different sequences are counted as different combinations.
```

Example 2:
```
Input: nums = [9], target = 3
Output: 0
```

Constraints:
* 1 <= nums.length <= 200
* 1 <= nums[i] <= 1000
* All the elements of nums are unique.
* 1 <= target <= 1000

<br />

## Sample C++ Code

We declare a dp variable as an array of long with length target + 1 since we will use up to the index target of it.

We set the very first cell to 1 and then loop with i from 1 to target (incuded) and:

* Set dp[i] to 0 (no need to go for an expensive isolated initialisation loop otherwise);
* Loop through all the elements n in nums and:

	- if i >= n add dp[i - n] to dp[i] (meaning we can reach that place from adding n to all the dp[i - n] solutions we computed before);
	- if dp[i] overflows the limits of a 32bit, we can just break, since that is not a viable solution.

Once done, we can just return dp[target].

```c
class Solution {
public:
    int combinationSum4(vector<int>& nums, int target) {
        // support variables
        long dp[target + 1];
        dp[0] = 1;
        // populating dp
        for (int i = 1; i <= target; i++) {
            // setting the initial value of a cell to 0
            dp[i] = 0;
            // updating dp[i] with all the previous combinations we can reach from there
            for (int n: nums) {
                if (i >= n) dp[i] += dp[i - n];
                if (dp[i] > INT_MAX) break;
            }
        }
        return dp[target];
    }
};
```


