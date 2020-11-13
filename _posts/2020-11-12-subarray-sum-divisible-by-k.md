---
layout: post
title:  "Subarray Sum Divisible By K Problem"
categories: [ Algorithm, Leetcode ]
tags: [ Hash Table ]
similar: [ Two Sum ]
featured: false
hidden: true
---

<br />

## Description

Given an array of integers **nums** and an integer **k**, return the total number of continuous subarrays whose sum is divisible by **k**.


Example: 
```
Input: nums = [4,5,0,-2,-3,1], k = 5
Output: 7
Explanation: There are 7 subarrays with a sum divisible by k = 5:
[4, 5, 0, -2, -3, 1], [5], [5, 0], [5, 0, -2, -3], [0], [0, -2, -3], [-2, -3]
```

<br />

## Solution

This problem is similar to the [`subarray sum equals k problem`]({% post_url 2020-11-11-subarray-sum-equals-k %}).

#### Brute Force Approach

A simple solution is to use the `brute force` approach. We can consider all possible subarrays and check whether the sum of each subarrays is divisible by *k*.

We can use a left pointer *l* and a right pointer *r* to enumerate all possible subarrays. We loop through each integer in the array *nums* with *l*. For each *l*, we iterate with *r* from *l*+1 to the end of the array. In the meantime, we use a *sum* variable to record the accumulative sum from *l* to *r*. If *sum* is divisible by *k*, we can increase the total count; otherwise, we can keep on searching.

The time complexity of this approach is O(n<sup>2</sup>), 
and the space complexity is O(1).


#### Hash Table Approach

The time complexity can be further reduced if we use a `hash table` to store intermediate results.

We loop through the array and use an *accu_sum* variable to store the accumulative sum. During the iteration, we calculate the modulo (*accu_sum* % *k*). We then store the modulo to a hash table as a key and the number of occurrence of this modulo as the value. 

During the iteration, if we have already found an *accu_sum* that has the same modulo with *k* as the current *accu_sum*, then the subarray between these two *accu_sum* has a sum divisible by *k*. 

We can check how many same modulo has occurred before, that will be the number of subarrays whose sums are divisible by *k*. Thus, we can add the value of this modulo in the hash table to the total count.

Here is a complete walk through of the `hash table` approach. The array *nums* is {4,5,0,-2,-3,1}, and *k* is 5.

```
|             nums            | accu_sum | modulo | ht
| 4  | 5  | 0  | -2 | -3 | 1  |     -    |    -   | (0,1)       <-- count = 0
  i                           |     4    |    4   | (0,1) (4,1) <-- No such subarray found
       i                      |     9    |    4   | (0,1) (4,2) <-- The sum of subarray [1..1] is divisible by k
                                                                    count = count+ht[modulo]-1 = 0+1 = 1
            i                 |     9    |    4   | (0,1) (4,3) <-- The sum of subarray [1..2], [2..2] is divisible by k
                                                                    count = count+ht[modulo]-1 = 1+2 = 3
                 i            |     7    |    2   | (0,1) (4,3) (2,1) <-- No such subarray found
                      i       |     4    |    4   | (0,1) (4,4) (2,1) <-- The sum of subarray [1..4] [2..4] [3..4] is divisible by k 
                                                                          count = count+ht[modulo]-1 = 3+3 = 6
                           i  |     5    |    0   | (0,2) (4,4) (2,1) <-- The sum of subarray [0..5] is divisible by k
                                                                          count = count+ht[modulo]-1 = 6+1 = 7 
```

The time complexity can be reduced to O(n), and the space complexity is O(k).

<br />

## Sample C++ Code
This is a C++ implementation of the hash table approach.
```c
#include <iostream>
#include <vector>
#include <algorithm>
#include <unordered_map>

using namespace std;

int subarraysDivByK(vector<int>& A, int K) {
    int len = A.size();
    unordered_map<int, int> ht;
    
    int accu_sum = 0;
    int count = 0;
    int modulo;
    ht[0] = 1;
    for (int i = 0; i < len; i ++) {
        accu_sum += A[i];
        modulo = accu_sum % K;
        if (modulo < 0)
            modulo += K;
        if (ht.find(modulo) == ht.end()) {
            ht[modulo] = 0;
        }
        count += ht[modulo];
        ht[modulo] ++;
    }
    return count;
}


int main() {
    vector<int> nums={4,5,0,-2,-3,1};
    int k = 5;
    cout << subarraysDivByK(nums, k) << endl;
}
```
