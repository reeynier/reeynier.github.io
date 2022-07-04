---
layout: post
title: "Contains Duplicate III Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Sliding Window, Sorting, Bucket Sort, Ordered Set ]
similar: [ Sliding Window ]
featured: false
hidden: false
excerpt: LeetCode 220. Given an integer array nums and two integers k and t, return true if there are two distinct indices i and j in the array such that abs(nums[i] - nums[j]) <= t and abs(i - j) <= k.

---

<br />

## Description

LeetCode Problem 220.

Given an integer array nums and two integers k and t, return true if there are two distinct indices i and j in the array such that abs(nums[i] - nums[j]) <= t and abs(i - j) <= k.

Example 1:
```
Input: nums = [1,2,3,1], k = 3, t = 0
Output: true
```

Example 2:
```
Input: nums = [1,0,1,1], k = 1, t = 2
Output: true
```

Example 3:
```
Input: nums = [1,5,9,1,5,9], k = 2, t = 3
Output: false
```

Constraints:
* 1 <= nums.length <= 2 * 10^4
* -2^31 <= nums[i] <= 2^31 - 1
* 0 <= k <= 10^4
* 0 <= t <= 2^31 - 1

<br />

## Sample C++ Code


```c
bool containsNearbyAlmostDuplicate(vector<int>& nums, int k, int t) {
    set<int> window; // set is ordered automatically 
    
    for (int i = 0; i < nums.size(); i++) {
        if (i > k) 
        	// keep the set contains nums i j at most k
        	window.erase(nums[i-k-1]); 

        // |x - nums[i]| <= t  ==> -t <= x - nums[i] <= t;
        // x-nums[i] >= -t ==> x >= nums[i]-t 
        auto pos = window.lower_bound(nums[i] - t); 

        // x - nums[i] <= t ==> |x - nums[i]| <= t    
        if (pos != window.end() && *pos - nums[i] <= t) 
        	return true;

        window.insert(nums[i]);
    }
    return false;
}
```


