---
layout: post
title: "Patching Array Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Greedy ]
similar: [ Greedy ]
featured: false
hidden: false
excerpt: LeetCode 330. Given a sorted integer array nums and an integer n, add/patch elements to the array such that any number in the range [1, n] inclusive can be formed by the sum of some elements in the array.

---

<br />

## Description

LeetCode Problem 330.

Given a sorted integer array nums and an integer n, add/patch elements to the array such that any number in the range [1, n] inclusive can be formed by the sum of some elements in the array.
Return the minimum number of patches required.
Example 1:
```
Input: nums = [1,3], n = 6
Output: 1
Explanation:
Combinations of nums are [1], [3], [1,3], which form possible sums of: 1, 3, 4.
Now if we add/patch 2 to nums, the combinations are: [1], [2], [3], [1,3], [2,3], [1,2,3].
Possible sums are 1, 2, 3, 4, 5, 6, which now covers the range [1, 6].
So we only need 1 patch.
```

Example 2:
```
Input: nums = [1,5,10], n = 20
Output: 2
Explanation: The two patches can be [2, 4].
```

Example 3:
```
Input: nums = [1,2,2], n = 5
Output: 0
```

Constraints:
* 1 <= nums.length <= 1000
* 1 <= nums[i] <= 10^4
* nums is sorted in ascending order.
* 1 <= n <= 2^31 - 1

<br />

## Sample C++ Code

We use a greedy approach. We first find `miss` which is the smallest sum in [0, n] that is missing. This means we can build all sums in [0, miss). For example, if the input is num = [1, 2, 4, 13, 43], and n = 100, then miss = 8.

Then in the given array, if we have a number `num <= miss` that is not used in building the sums in [0, miss), we can add it to build all sums in [0, miss+num). If we don't have such a number, then we add `miss` to the array to maximize the range of sums we can reach. 

In the example, we first add 8 to the array, so we can build all sums in [0, 16). As we have 13 that is not used in building sums in [0, 16), we can use it to build sums in [0, 29). Then we insert 29 in the array. This extends the range of sums to [0, 58). Next we consider 43 and extend the range to [0, 101). Then we are done.

```c
int minPatches(vector<int>& nums, int n) {
    long miss = 1, added = 0, i = 0;
    while (miss <= n) {
        if (i < nums.size() && nums[i] <= miss) {
            miss += nums[i++];
        } else {
            miss += miss;
            added++;
        }
    }
    return added;
}
```


