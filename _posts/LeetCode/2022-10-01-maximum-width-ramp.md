---
layout: post
title: "Maximum Width Ramp Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Stack, Monotonic Stack ]
similar: [ Stack ]
featured: false
hidden: false
excerpt: LeetCode 962. A ramp in an integer array nums is a pair (i, j) for which i < j and nums[i] <= nums[j]. The width of such a ramp is j - i.

---

<br />

## Description

LeetCode Problem 962.

A ramp in an integer array nums is a pair (i, j) for which i < j and nums[i] <= nums[j]. The width of such a ramp is j - i.

Given an integer array nums, return the maximum width of a ramp in nums. If there is no ramp in nums, return 0.

Example 1:
```
Input: nums = [6,0,8,2,1,5]
Output: 4
Explanation: The maximum width ramp is achieved at (i, j) = (1, 5): nums[1] = 0 and nums[5] = 5.
```

Example 2:
```
Input: nums = [9,8,1,0,1,9,4,0,4,1]
Output: 7
Explanation: The maximum width ramp is achieved at (i, j) = (2, 9): nums[2] = 1 and nums[9] = 1.
```

Constraints:
* 2 <= nums.length <= 5 * 10^4
* 0 <= nums[i] <= 5 * 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maxWidthRamp(vector<int>& nums) {
        if (nums.size() < 2)
            return 0;
        int ans = 0, n = nums.size()-1;
        stack<int> st;
        for (int j = 0; j < nums.size(); j++) {
            if (st.empty() || nums[j] < nums[st.top()])
                st.push(j);
        }
        for (int i = n; i > ans; i--) {
            while (!st.empty() && nums[i] >= nums[st.top()]) {
                ans = max(ans, i - st.top());
                st.pop();
            }
        }
        return ans;
    }
};
```


