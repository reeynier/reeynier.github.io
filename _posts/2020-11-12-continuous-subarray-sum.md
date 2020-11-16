---
layout: post
title:  "Continuous Subarray Sum Problem"
categories: [ Algorithm ]
tags: [ Hash Table, Leetcode ]
similar: [ Two Sum ]
featured: false
hidden: false
---

<br />

## Description

Given an array of non-negative integers **nums** and an integer **k**, check if the array has a continuous subarray of size at least 2 that sums up to a multiple of **k**.


Example: 
```
Input: nums = [23, 2, 4, 6, 7], k = 6
Output: True
Explanation: [2, 4] is a continuous subarray of size 2 and sums up to 6.
```

<br />

## Solution

This problem is similar to the [`subarray sum divisible by k problem`]({% post_url 2020-11-12-subarray-sum-divisible-by-k %}).

#### Brute Force Approach

A simple solution is to use the `brute force` approach. We can consider all possible subarrays and check whether the sum of each subarrays is divisible by *k*.

We can use a left pointer *l* and a right pointer *r* to enumerate all possible subarrays. We loop through each integer in the array *nums* with *l*. For each *l*, we iterate with *r* from *l*+1 to the end of the array. In the meantime, we use a *sum* variable to record the accumulative sum from *l* to *r*. If *sum* is divisible by *k* and the distance between *l* and *r* is greater than 1, we return true; otherwise, we keep on searching. If we cannot find one such subarray, we return false.

The time complexity of this approach is O(n<sup>2</sup>), 
and the space complexity is O(1).


#### Hash Table Approach

The time complexity can be further reduced if we use a `hash table` to store intermediate results. The solution is similar to the solution to the [`subarray sum divisible by k problem`]({% post_url 2020-11-12-subarray-sum-divisible-by-k %}). The only difference is that instead of storing the (modulo, count) pair in the hash table, we store the (modulo, index) pair, because we only need to find out whether such a subarray exists, but not how many such subarrays.

We loop through the array and use an *accu_sum* variable to store the accumulative sum. During the iteration, we calculate the modulo (*accu_sum* % *k*). We then store the modulo to a hash table as a key and the index of the current element as the value. 

During the iteration, if we have already found an *accu_sum* that has the same modulo with *k* as the current *accu_sum*, then the subarray between these two *accu_sum* has a sum divisible by *k*. 

We can check the distance between the index of the current element and the index of the previous element to see whether the size of the subarray is at least two. If so, we can return true. Otherwise, we keep on searching.


The time complexity can be reduced to O(n), and the space complexity is O(k).

<br />

## Sample C++ Code

This is a C++ implementation of the hash table approach.

```c
#include <iostream>
#include <vector>
#include <algorithm>
#include <unordered_map>
#include <climits>

using namespace std;

bool checkSubarraySum(vector<int>& nums, int k) {
    int len = nums.size();
    if (len < 2)
        return false;
    unordered_map<int, int> ht;
    
    int accu_sum = 0;
    ht[0] = -1;
    if (k == 0) k = INT_MAX;
    for (int i = 0; i < len; i ++) {
        accu_sum += nums[i];
        if (ht.find(accu_sum % k) != ht.end()) {
            if (i - ht[accu_sum % k] > 1)
                return true;
        } else {
            ht[accu_sum % k] = i;
        }
    }
    return false;
}


int main() {
    vector<int> nums={23, 2, 4, 6, 7};
    int k = 6;
    cout << checkSubarraySum(nums, k) << endl;
}
```
