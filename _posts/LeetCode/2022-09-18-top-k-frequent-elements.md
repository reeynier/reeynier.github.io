---
layout: post
title: "Top K Frequent Elements Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Divide and Conquer, Sorting, Heap ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 347. Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

---

<br />

## Description

LeetCode Problem 347.

Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

Example 1:
```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

Example 2:
```
Input: nums = [1], k = 1
Output: [1]
```

Constraints:
* 1 <= nums.length <= 10^5
* k is in the range [1, the number of unique elements in the array].
* It is guaranteed that the answer is unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    static bool cmp (const pair<int, int> &a, const pair<int, int> &b) {
        return a.second > b.second;
    }
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int, int> ht;
        vector<pair<int, int>> v;
        for (int i = 0; i < nums.size(); i ++) {
            if (ht.find(nums[i]) == ht.end())
                ht[nums[i]] = 0;
            ht[nums[i]] ++;
        }
        for (auto m : ht) {
            v.push_back({m.first, m.second});
        }
        sort(v.begin(), v.end(), cmp);
        
        vector<int> ans;
        for (int i = 0; i < k; i ++) {
            ans.push_back(v[i].first);
        }
        
        return ans;
    }
};
```


