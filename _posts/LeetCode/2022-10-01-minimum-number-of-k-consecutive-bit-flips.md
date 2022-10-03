---
layout: post
title: "Minimum Number Of K Consecutive Bit Flips Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Bit Manipulation, Queue, Sliding Window, Prefix Sum ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 995. You are given a binary array nums and an integer k.

---

<br />

## Description

LeetCode Problem 995.

You are given a binary array nums and an integer k.

A k-bit flip is choosing a subarray of length k from nums and simultaneously changing every 0 in the subarray to 1, and every 1 in the subarray to 0.

Return the minimum number of k-bit flips required so that there is no 0 in the array. If it is not possible, return -1.

A subarray is a contiguous part of an array.

Example 1:
```
Input: nums = [0,1,0], k = 1
Output: 2
Explanation: Flip nums[0], then flip nums[2].
```

Example 2:
```
Input: nums = [1,1,0], k = 2
Output: -1
Explanation: No matter how we flip subarrays of size 2, we cannot make the array become [1,1,1].
```

Example 3:
```
Input: nums = [0,0,0,1,0,1,1,0], k = 3
Output: 3
Explanation: 
Flip nums[0],nums[1],nums[2]: nums becomes [1,1,1,1,0,1,1,0]
Flip nums[4],nums[5],nums[6]: nums becomes [1,1,1,1,1,0,0,0]
Flip nums[5],nums[6],nums[7]: nums becomes [1,1,1,1,1,1,1,1]
```

Constraints:
* 1 <= nums.length <= 10^5
* 1 <= k <= nums.length

<br />

## Sample C++ Code


```c
class Solution {
public:
    // If we encounter a '0', it must be flipped and hence we increase ans by 1.
    // If we don't get k elements including this element, 
    // that means we can't change this element from 0 to 1 and we have to return -1.
    // if flip[i]%2==0 it means i th element has been flipped even number of times 
    // and is in the same state as mentioned in ar[i].
    // Flipping is done when ar[i] has 0 and ar[i] is in original state of 
    // when ar[i] is 1 and ar[i] is in flipped state.
    int minKBitFlips(vector<int>& ar, int k) {
        int n = ar.size(), ans = 0;
        //  flip[i] stores how many times current index(i) is flipped
        vector<int> flip(n, 0); 
        for (int i = 0; i < n; i++) {
            if (i) 
                flip[i] += flip[i-1];
            if ((flip[i]%2 && ar[i]) || (flip[i]%2 == 0 && !ar[i])) {
                ans++;
                // ar[i] must be flipped
                // ar[i+k] is not flipped
                flip[i]++;
                if (i + k > n) 
                    return -1;
                if (i + k < n) 
                    flip[i+k]--;
            }
        }
        return ans;
    }
};
```


