---
layout: post
title:  "Two Sum Less Than K Problem"
categories: [ Algorithm, Solution ]
tags: [ Two Pointer ]
similar: [ Two Sum ]
featured: false
hidden: true
---

<br />

## Description

Given an array of integers **nums** and an integer **k**, return the maximum **s** such that there exists **i < j** with **nums[i] + nums[j] = s** and **s < k**. If no such **i, j, s** exists, return **-1**.


Example: 
```
Input: nums = [34,23,1,24,75,33,54,8], k = 60
Output: 58
Explanation: We can use 34 and 24 to sum 58 which is less than 60.
```

<br />

## Solution


#### Brute Force Approach

A simple solution is to use the `brute force` approach. 

We loop through each element *x* in the array. For each element, 
we loop through each of the rest elements *x'* to see whether (*x* + *x'* < *k*), 
and update *s* if (*x* + *x'* > *s*). 

The time complexity of this approach is O(n<sup>2</sup>), 
and the space complexity is O(1).




#### Two Pointer Approach

We can use the `two pointer` approach similar to the [`three sum problem`]({% post_url 2020-11-10-three-sum %}).

We first sort the array in ascending order, the time complexity of this step is O(nlogn).

We then set two pointers *l* and *r* pointing to the first and last element of the array, respectively. If the sum of the two elements pointed by *l* and *r* are greater or equal to *k*, that means the right element is too big (even the smallest left element cannot satisfy the requirement), then we move the right element one step to the left. Otherwise, we check whether the sum is larger than *s*, if so, we update *s* with the new sum. We then move the left pointer one step to the right.

When *l* and *r* meet, we can stop the search.

The time complexity can be reduced to O(nlogn), and the space complexity is O(n).

<br />

## Sample C++ Code

This is a C++ implementation of the two pointer approach.

```c
#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>

using namespace std;

int twoSumLessThanK(vector<int>& nums, int k) {
    int s = INT_MIN;
    int l = 0, r = nums.size()-1;
    sort(nums.begin(), nums.end());
    while (l < r) {
        if (nums[l] + nums[r] >= k) {
            r --;
        } else {
            s = max(s, nums[l]+nums[r]);
            l ++;
        }
    }
    return s;
}


int main() {
    vector<int> nums={34,23,1,24,75,33,54,8};
    int k = 60;
    cout << twoSumLessThanK(nums, k) << endl;
}
```
