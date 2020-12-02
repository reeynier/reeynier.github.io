---
layout: post
title:  "Subarray Product Less Than K Problem"
categories: [ Algorithm ]
tags: [ Two Pointer, Leetcode ]
similar: [ Two Sum ]
featured: false
hidden: false
excerpt: LeetCode 713. Given an array of positive integers **nums** and an integer **k**, return the total number of continuous subarrays where the product of all the elements in the subarray is less than **k**.
---

<br />

## Description

LeetCode Problem 713. Given an array of positive integers **nums** and an integer **k**, return the total number of continuous subarrays where the product of all the elements in the subarray is less than **k**.


Example: 
```
Input: nums = [10, 5, 2, 6], k = 100
Output: 8
Explanation: The 8 subarrays that have product less than 100 are: [10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6]. 
The subarray [10, 5, 2] is not included as the product of 100 is not strictly less than k.
```

<br />

## Solution


#### Brute Force Approach

A simple solution is to use the `brute force` approach. We can consider all possible subarrays and check the product of each subarrays with the given integer *k*.

We can use a left pointer *l* and a right pointer *r* to enumerate all possible subarrays. We loop through each integer in the array *nums* with *l*. For each *l*, we iterate with *r* from *l*+1 to the end of the array. In the meantime, we use a *product* variable to record the accumulative product from *l* to *r*. If *product* is less than *k*, we can increase the total count; otherwise, we can keep on searching. 

The time complexity of this approach is O(n<sup>2</sup>), 
and the space complexity is O(1).


#### Two Pointer Approach

There are a lot of unnecessary calculation in the above approach. For example, when the *product* is equal to or greater than *k*, we do not need to continue the search for the rest of the array. We can optimize the brute force approach by reducing unnecessary calculations. 

We keep two pointers: left *l* and right *r*. We iterate the right pointer through the array. The left pointer starts from the first element. When the *product* of the elements between the two pointers is greater or equal to *k*, we move the left pointer *l* to the right until the *product* is less than *k*. Then the subarrays ending at the element pointed by *r* satisfy the requirement and should be counted (the number of these subarrays is (*r*-*l*+1). 


Here is a complete walk through of the `two pointer` approach. The array *nums* is {10, 5, 2, 6}, and *k* is 100.

```
|        nums       | product | count |
| 10 | 5  | 2  | 6  |    1    |   0   |  Initialization
  lr                |    10   |   1   |  product<100 => count = count+(r-l+1) = 0+(0-0+1) = 1 
  l    r            |    50   |   3   |  product<100 => count = count+(r-l+1) = 1+(1-0+1) = 3
  l         r       |   100   |   3   |  product=100 => product/=nums[l], l++, until product<100
       l    r       |    10   |   5   |  product<100 => count = count+(r-l+1) = 3+(2-1+1) = 5
       l         r  |    60   |   8   |  product<100 => count = count+(r-l+1) = 5+(3-1+1) = 8
```

The time complexity can be reduced to O(n), while the 
space complexity is still O(1).

<br />

## Sample C++ Code

This is a C++ implementation of the two pointer approach.

```c
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int numSubarrayProductLessThanK(vector<int>& nums, int k) {
    if (k <= 1) return 0;
    int product = 1, count = 0;
    int l = 0;
    for (int r = 0; r < nums.size(); r ++) {
        product *= nums[r];
        while (product >= k) { 
            product /= nums[l];
            l ++;
        }
        count += r - l + 1;
    }
    return count;
}


int main() {
    vector<int> nums={10, 5, 2, 6};
    int k = 100;
    cout << numSubarrayProductLessThanK(nums, k) << endl;
}
```
