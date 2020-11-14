---
layout: post
title:  "Subarray Sum Equals K Problem"
categories: [ Algorithm, Leetcode ]
tags: [ Hash Table ]
similar: [ Two Sum ]
featured: false
hidden: false
---

<br />

## Description

Given an array of integers **nums** and an integer **k**, return the total number of continuous subarrays whose sum equals to **k**.


Example: 
```
Input: nums = [1, 2, 3], k = 3
Output: 2
```

<br />

## Solution

This problem is similar to the [`two sum problem`]({% post_url 2020-11-09-two-sum %}).

#### Brute Force Approach

A simple solution is to use the `brute force` approach. We can consider all possible subarrays and check the sum of each subarrays with the given integer *k*.

We can use a left pointer *l* and a right pointer *r* to enumerate all possible subarrays. We loop through each integer in the array *nums* with *l*. For each *l*, we iterate with *r* from *l*+1 to the end of the array. In the meantime, we use a *sum* variable to record the accumulative sum from *l* to *r*. If *sum* equals *k*, we can increase the total count; otherwise, we can keep on searching.

The time complexity of this approach is O(n<sup>2</sup>), 
and the space complexity is O(1).


#### Hash Table Approach

The time complexity can be further reduced if we use a `hash table` to store intermediate results (similar to the [`two sum problem`]({% post_url 2020-11-09-two-sum %})).

We loop through the array and use an *accu_sum* variable to store the accumulative sum. For each distinctive *accu_sum*, we use a hash table to store how many times this *accu_sum* has occurred. 

During the iteration, if the current *accu_sum* is greater than *k*, and (*accu_sum*-*k*) exists in the hash table, it means the sum of integers in the array between (*accu_sum*-*k*) and *accu_sum* is *k*. So we have found solutions. The number of possible subarrays depends on how many (*accu_sum*-*k*) are there (stored as the value in the hash table). We can increase the total count with this value.

After we finish the iteration, we can find the number of all possible subarrays.

One thing to note is that before we start the iteration, we store the key-value pair (0, 1) to the hash table. In that case, if the accumulative sum is *k*, we will have 1 answer at least (unless there are other subarrays with *accu_sum* to be 0).


Here is a complete walk through of the `hash table` approach. The array *nums* is {1, 2, 2, 1, 3}, and *k* is 3.

```
|       nums        | accu_sum | count | ht (accu_sum, cnt)
| 1 | 2 | 2 | 1 | 3 |     -    |   -   | (0,1)
  i                 |     1    |   0   | (0,1) (1,1)        <--  accu_sum < k
      i             |     3    |   1   | (0,1) (1,1) (3,1)  <--  ht[accu_sum-k] = ht[0] = 1 => count = 1
          i         |     5    |   1   | (0,1) (1,1) (3,1)  <--  ht[accu_sum-k] = ht[2] doesn't exist => count = 1
                    |          |       | (5,1)
              i     |     6    |   2   | (0,1) (1,1) (3,1)  <--  ht[accu_sum-k] = ht[3] = 1 => count = 2
                    |          |       | (5,1) (6,1)
                  i |     9    |   3   | (0,1) (1,1) (3,1)  <--  ht[accu_sum-k] = ht[6] = 1 => count = 3
                    |          |       | (5,1) (6,1) (9,1)
```

The time complexity can be reduced to O(n), while the 
space complexity is still O(n).

<br />

## Sample C++ Code

This is a C++ implementation of the hash table approach.

```c
#include <iostream>
#include <vector>
#include <algorithm>
#include <unordered_map>

using namespace std;

int subarraySum(vector<int>& nums, int k) {
    int len = nums.size();
    unordered_map<int, int> ht;
    
    int accu_sum = 0;
    int count = 0;
    ht[0] = 1;
    for (int i = 0; i < len; i ++) {
        accu_sum += nums[i];
        if (ht.find(accu_sum) == ht.end())
            ht[accu_sum] = 0;
        if (ht.find(accu_sum-k) != ht.end()) {
            count += ht[accu_sum-k];
        }
        ht[accu_sum] += 1;

    }
    
    return count;
}


int main() {
    vector<int> nums={1,2,2,1,3};
    int k = 3;
    cout << subarraySum(nums, k) << endl;
}
```
