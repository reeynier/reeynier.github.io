---
layout: post
title: "Maximum Gap Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Sorting, Bucket Sort, Radix Sort ]
similar: [ Sorting ]
featured: false
hidden: false
excerpt: LeetCode 164. Given an integer array nums, return the maximum difference between two successive elements in its sorted form. If the array contains less than two elements, return 0.

---

<br />

## Description

LeetCode Problem 164.

Given an integer array nums, return the maximum difference between two successive elements in its sorted form. If the array contains less than two elements, return 0.

You must write an algorithm that runs in linear time and uses linear extra space.

Example 1:
```
Input: nums = [3,6,9,1]
Output: 3
Explanation: The sorted form of the array is [1,3,6,9], either (3,6) or (6,9) has the maximum difference 3.
```

Example 2:
```
Input: nums = [10]
Output: 0
Explanation: The array contains less than 2 elements, therefore return 0.
```

Constraints:
* 1 <= nums.length <= 10^5
* 0 <= nums[i] <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    int maximumGap(vector<int>& nums) {
        int mn = INT_MAX, mx = INT_MIN;
        int n = nums.size();
        if (n < 2)
        	return 0;
        for (int i=0;i<n;++i) {
        	mn = min(nums[i], mn);
        	mx = max(nums[i], mx);
		}
		if (mx == mn)
			return 0;
		double bucket = (mx - mn + 0.0) / n; 
		vector<int> big(n, -1); 
		vector<int> small(n, -1);  
		for (int i=0;i<n;++i) {
			int index = (nums[i] - mn) / bucket;
			if (index >= n) 
				index = n - 1; 
			
			if (big[index] == -1) {
				big[index] = small[index] = nums[i];
			}
			else {
				big[index] = max(big[index], nums[i]);
				small[index] = min(small[index], nums[i]);
			}
		}
		int result = 0;
		int s = mn, b = mn;
		for (int i=0;i<n;++i) { 
			if (big[i] == -1)
				continue;
			result = max(small[i] - b, result); 
			s = small[i];
			b = big[i];
		}
		return result;
    }
};
```


