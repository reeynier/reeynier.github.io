---
layout: post
title: "Tallest Billboard Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 956. You are installing a billboard and want it to have the largest height. The billboard will have two steel supports, one on each side. Each steel support must be an equal height.

---

<br />

## Description

LeetCode Problem 956.

You are installing a billboard and want it to have the largest height. The billboard will have two steel supports, one on each side. Each steel support must be an equal height.

You are given a collection of rods that can be welded together. For example, if you have rods of lengths 1, 2, and 3, you can weld them together to make a support of length 6.

Return the largest possible height of your billboard installation. If you cannot support the billboard, return 0.

Example 1:
```
Input: rods = [1,2,3,6]
Output: 6
Explanation: We have two disjoint subsets {1,2,3} and {6}, which have the same sum = 6.
```

Example 2:
```
Input: rods = [1,2,3,4,5,6]
Output: 10
Explanation: We have two disjoint subsets {2,3,5} and {4,6}, which have the same sum = 10.
```

Example 3:
```
Input: rods = [1,2]
Output: 0
Explanation: The billboard cannot be supported, so we return 0.
```

Constraints:
* 1 <= rods.length <= 20
* 1 <= rods[i] <= 1000
* sum(rods[i]) <= 5000

<br />

## Sample C++ Code


```c
class Solution {
public:
    int tallestBillboard(vector<int>& nums) {
        int sum = accumulate(nums.begin(), nums.end(), 0);
        vector<int> dp(sum + 1, -1), curr;
        dp[0] = 0;
        for (int &el : nums) {
            // storing the immediate calculated values
            curr = dp;
            for (int i = 0; i <= sum - el; ++i) {
                // not computed still now, so skip it
                if (curr[i] < 0)
                    continue;
                // putting rod into heighest side
                dp[i + el] = max(dp[i + el], curr[i]);
                // putting rod into smallest side
                dp[abs(i - el)] = max(dp[abs(i - el)], curr[i] + min(i, el));
            }
        }
        // we need equal sizes so diff =0 will be my ans
        return dp[0];
    }
};
```


