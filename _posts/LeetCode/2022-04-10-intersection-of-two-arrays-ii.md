---
layout: post
title: "Intersection Of Two Arrays II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Two Pointers, Binary Search, Sorting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 350. Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in any order.

---

<br />

## Description

LeetCode Problem 350.

Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in any order.

Example 1:
```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```

Example 2:
```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
Explanation: [9,4] is also accepted.
```

Constraints:
* 1 <= nums1.length, nums2.length <= 1000
* 0 <= nums1[i], nums2[i] <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        map<int, int> ht;
        for (int i = 0; i < nums1.size(); i ++) {
            if (ht.find(nums1[i]) == ht.end()) 
                ht[nums1[i]] = 0;
            ht[nums1[i]] ++;
        }
        vector<int> ans;
        for (int i = 0; i < nums2.size(); i ++) {
            if (ht.find(nums2[i]) != ht.end()) {
                if (ht[nums2[i]] > 0) {
                    ans.push_back(nums2[i]);
                    ht[nums2[i]] --;
                }
            }
        }
        return ans;
    }
};
```


