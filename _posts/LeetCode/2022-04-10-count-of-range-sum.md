---
layout: post
title: "Count Of Range Sum Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search, Divide and Conquer, Binary Indexed Tree, Segment Tree, Merge Sort, Ordered Set ]
similar: [ Merge Sort ]
featured: false
hidden: false
excerpt: LeetCode 327. Given an integer array nums and two integers lower and upper, return the number of range sums that lie in [lower, upper] inclusive.

---

<br />

## Description

LeetCode Problem 327.

Given an integer array nums and two integers lower and upper, return the number of range sums that lie in [lower, upper] inclusive.

Range sum S(i, j) is defined as the sum of the elements in nums between indices i and j inclusive, where i <= j.

Example 1:
```
Input: nums = [-2,5,-1], lower = -2, upper = 2
Output: 3
Explanation: The three ranges are: [0,0], [2,2], and [0,2] and their respective sums are: -2, -1, 2.
```

Example 2:
```
Input: nums = [0], lower = 0, upper = 0
Output: 1
```

Constraints:
* 1 <= nums.length <= 10^5
* -2^31 <= nums[i] <= 2^31 - 1
* -10^5 <= lower <= upper <= 10^5
* The answer is guaranteed to fit in a 32-bit integer.

<br />

## Sample C++ Code


```c
class Solution {
private:    
    int mergeSort(vector<long long>&sum, int left, int right, int lower, int upper) {
        int mid, i, res, j, k;
        if(left>right) 
        	return 0;
        if(left==right) 
        	return ( (sum[left]>=lower) && (sum[left]<=upper) )?1:0;
        else {
            vector<long long> temp(right-left+1,0);
            mid = (left+right)/2;
            // merge sort two halfs first, be careful about how to divide [left, mid] and [mid+1, right]
            res = mergeSort(sum, left,mid, lower, upper) + mergeSort(sum, mid+1,right, lower, upper); 
            for(i=left, j=k=mid+1; i<=mid; ++i) { 
            	// count the valid ranges [i,j], where i is in the first half and j is in the second half
                while(j<=right && sum[j]-sum[i]<lower)  ++j;
                while(k<=right && sum[k]-sum[i]<=upper) ++k;
                res +=k-j;
            }
            for(i=k=left, j=mid+1; k<=right; ++k) 
            	//merge the sorted two halfs
                temp[k-left] = (i<=mid) && (j>right || sum[i]<sum[j])?sum[i++]:sum[j++]; 
            for(k=left; k<=right; ++k) 
            	// copy the sorted results back to sum
                sum[k] = temp[k-left]; 
            return res;
        }
    }
public:
    int countRangeSum(vector<int>& nums, int lower, int upper) {
         int len = nums.size(), i;
         vector<long long> sum(len+1, 0);
         for(i=1; i<=len; ++i) 
         	sum[i] = sum[i-1]+nums[i-1];
         return mergeSort(sum, 1, len, lower, upper);
    }
};
```


