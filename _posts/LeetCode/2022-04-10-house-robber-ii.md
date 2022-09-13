---
layout: post
title: "House Robber II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Dynamic Programming ]
similar: [ Dynamic Programming ]
featured: false
hidden: false
excerpt: LeetCode 213. You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, andit will automatically contact the police if two adjacent houses were broken into on the same night.

---

<br />

## Description

LeetCode Problem 213.

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

Example 1:
```
Input: nums = [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.
```

Example 2:
```
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
```

Example 3:
```
Input: nums = [1,2,3]
Output: 3
```

Constraints:
* 1 <= nums.length <= 100
* 0 <= nums[i] <= 1000

<br />

## Sample C++ Code

Since we cannot rob both the first house and the last house, we can create two vectors, one excluding the first house and one excluding the last house. Then we can apply the same approach as in the original House Robber (LeetCode 198) problem to the two vectors to generate the best solution.

```c
class Solution {
public:
    int robOriginal(vector<int>& nums) {
        int a = 0, b = 0, res = 0;
        
        for(int i = 0; i < nums.size(); ++i){
            res = max(b + nums[i], a);
            b = a;
            a = res;
        }
        
        return res;
    }

    int rob(vector<int>& nums) {
        if(nums.empty()) return 0;
        if(nums.size() == 1) return nums[0];
        
        vector<int> numsA(nums.begin() + 1, nums.end());
        vector<int> numsB(nums.begin(), nums.end()-1);
        
        return max(robOriginal(numsA), robOriginal(numsB));
    }
};
```


