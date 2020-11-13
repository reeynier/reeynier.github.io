---
layout: post
title:  "Two Sum Input Array Is Sorted Problem"
categories: [ Algorithm, Leetcode ]
tags: [ Two Pointer ]
similar: [ Two Sum ]
featured: false
hidden: true
---

<br />

## Description

Given an array of integers **nums** sorted in ascending order, and an integer **target**, return indices of the two numbers such that they add up to target.

Example: 
```
Input: nums = [2,7,11,15], target = 9.
Output: [0,1].
Explanation: As nums[0] + nums[1] = 2 + 7 = 9, we return [0, 1].
```

<br />

## Solution

This problem is similar to the [`two sum problem`]({% post_url 2020-11-09-two-sum %}), the [`three sum problem`]({% post_url 2020-11-10-three-sum %}), and the [`two sum less than k problem`]({% post_url 2020-11-11-two-sum-less-than-k %}).

#### Brute Force Approach

A simple solution is to use the `brute force` approach. 

We loop through each element *x* in the array. For each element, 
we loop through each of the rest elements *x'* to see whether (*x* + *x'* = *k*).

The time complexity of this approach is O(n<sup>2</sup>), 
and the space complexity is O(1).


#### Two Pointer Approach

We can use the `two pointer` approach similar to the [`three sum problem`]({% post_url 2020-11-10-three-sum %}).

We set two pointers *l* and *r* pointing to the first and last element of the array, respectively. If the sum of the two elements pointed by *l* and *r* is greater than *target*, that means the right element is too big (even the smallest left element cannot satisfy the requirement), then we move the right pointer one step to the left. If the sum of the two elements pointed by *l* and *r* is smaller than *target*, that means the left element is too small (even the biggest right element cannot satisfy the requirement), then we move the left pointer one step to the right. If the sum equals to *target*, we find the solution and return the pointers.

The time complexity can be reduced to O(n), and the space complexity is O(1).

<br />

## Sample C++ Code

This is a C++ implementation of the two pointer approach.

```c
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> twoSum(vector<int>& numbers, int target) {
    int len = numbers.size();
    if (len == 0) return {};
    
    int l, r;
    l = 0, r = len - 1;
    while (l <= r) {
        if (numbers[l] + numbers[r] < target) {
            l ++;
        } else if (numbers[l] + numbers[r] == target) {
            break;
        } else {
            r --;
        }
    }
    return {l, r};
}


int main() {
    vector<int> nums={2,7,11,15};
    int target = 9;
    vector<int> ans;
    ans = twoSum(nums, target);
    cout << ans[0] << " " << ans[1] << endl;
}
```
