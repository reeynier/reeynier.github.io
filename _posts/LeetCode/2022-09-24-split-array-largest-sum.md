---
layout: post
title: "Split Array Largest Sum Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search, Dynamic Programming, Greedy ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 410. Given an array nums which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays.

---

<br />

## Description

LeetCode Problem 410.

Given an array nums which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays.

Write an algorithm to minimize the largest sum among these m subarrays.

Example 1:
```
Input: nums = [7,2,5,10,8], m = 2
Output: 18
Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.
```

Example 2:
```
Input: nums = [1,2,3,4,5], m = 2
Output: 9
```

Example 3:
```
Input: nums = [1,4,4], m = 3
Output: 4
```

Constraints:
* 1 <= nums.length <= 1000
* 0 <= nums[i] <= 10^6
* 1 <= m <= min(50, nums.length)

<br />

## Sample C++ Code

The idea for this problem is to use binary search. Instead of list all possible positions of the cut, we list all possible max sums of the subarrays. Because there is no clear relationship when you find out i subarrays, what is the best solutions for i+1 subarrays.

The range of possible answers should be between max(nums[i]) and sum(nums[i]). The higher bar is because when there is one subarray, this is the sum. We won't find a larger sum here. The lower bar goes to the other extreme, every subarray only contains 1 integer. This is the lower bar because the max integer should be within one subarray, and the sum of this subarray will be larger or equal to this integer. So, all max sum will be equal or larger than this sum, as this one is one possible value.
    
After we find out the range of the two extremes of the max sum, we use binary search to figure out what is the smallest max sum. We test whether a max sum is possible in this way. We divide the array into subarrays, and make sure the sum of each subarray is less or equal than this possible value. Then we count how many subarrays are there. If the number of subarrays is less or equal to m, that means this possible value can be a max sum here. Note that this is just a possible max sum, we are not sure it can definite be valid. (To be valid, there must be a subarray whose sum is this possible value.) So that means the higher bar is too high, we should lower the higher bar. This is because with m subarrays, this possible value is reachable, we won't get a larger max sum. (If we have less than m subarrays, the max sum should be larger, and that is still less than this possible, so if we have m subarrays, because we further cut the arrays, the max sum should be less or equal than the current one.) If the number of subarrays is greater than m, that means the lower bar is too low, we should raise it. This is because we need more than m subarrays to reach this low possible value, if we only can have m subarrays, our max sum will be larger than this one, so this possible value is too low.
    
The final question is how can we make sure, after using this binary search, the final value is a valid one. When we narrow down the scope of the max sum, we did not check if they are valid. This is because if the final result is not a valid value, that means the final result != max sum of the current separation of subarrays. If the final result > max sum, then for the valid max sum, count <= m is still true, then the search won't stop. And also true for final result < max sum.

```c
class Solution {
public:
    int count(vector<int> &nums, long long mid) {
        long long sum = 0;
        int count = 0;
        for (int i = 0; i < nums.size(); i ++) {
            sum += nums[i];
            if (sum > mid) {
                count ++;
                sum = nums[i];
            }
        }
        count ++;
        return count;
    }
    
    int splitArray(vector<int>& nums, int m) {
        long long sum = 0;
        int maxnum = 0;
        int len = nums.size();
        for (int i = 0; i < len; i ++) {
            sum += nums[i];
            if (maxnum < nums[i])
                maxnum = nums[i];
        }
        
        if (m == 1) 
            return sum;
        
        long long left = maxnum, right = sum;
        long long mid = (left + right) / 2;
        long long ans;
        
        while (left <= right) { 
            // we should check the case that "left == right"
            // otherwise, we will miss checking one case when (mid == right), 
            // whether this works or not
            mid = (left + right) / 2;
            if (count(nums, mid) <= m) {
                // here we should use <=, because we want to include the situation 
                // that count == m, this will be the answer
                ans = mid;
                right = mid - 1;
            }
            else
                left = mid + 1;
        }
        return ans;
    }
};
```


