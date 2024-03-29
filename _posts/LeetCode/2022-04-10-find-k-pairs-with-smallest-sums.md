---
layout: post
title: "Find K Pairs With Smallest Sums Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Heap ]
similar: [ Heap ]
featured: false
hidden: false
excerpt: LeetCode 373. You are given two integer arrays nums1 and nums2 sorted in ascending order and an integer k.

---

<br />

## Description

LeetCode Problem 373.

You are given two integer arrays nums1 and nums2 sorted in ascending order and an integer k.
Define a pair (u, v) which consists of one element from the first array and one element from the second array.

Return the k pairs (u_1, v_1), (u_2, v_2), ..., (u_k, v_k) with the smallest sums.

Example 1:
```
Input: nums1 = [1,7,11], nums2 = [2,4,6], k = 3
Output: [[1,2],[1,4],[1,6]]
Explanation: The first 3 pairs are returned from the sequence: [1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]
```

Example 2:
```
Input: nums1 = [1,1,2], nums2 = [1,2,3], k = 2
Output: [[1,1],[1,1]]
Explanation: The first 2 pairs are returned from the sequence: [1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]
```

Example 3:
```
Input: nums1 = [1,2], nums2 = [3], k = 3
Output: [[1,3],[2,3]]
Explanation: All possible pairs are returned from the sequence: [1,3],[2,3]
```

Constraints:
* 1 <= nums1.length, nums2.length <= 10^5
* -10^9 <= nums1[i], nums2[i] <= 10^9
* nums1 and nums2 both are sorted in ascending order.
* 1 <= k <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<vector<int>> kSmallestPairs(vector<int>& nums1, vector<int>& nums2, int k) {
        vector<vector<int>> ans;
        priority_queue<vector<int>, vector<vector<int>>, greater<vector<int>> > pq;
        
        if (nums1.empty() || nums2.empty())
            return ans;
        
        for (int i = 0; i < nums1.size(); i ++) {
            for (int j = 0; j < nums2.size(); j ++) {
                pq.push({nums1[i]+nums2[j], nums1[i], nums2[j]});
            }
        }
        
        while (!pq.empty() && k > 0) {
            k --;
            vector<int> temp;
            temp.push_back(pq.top()[1]);
            temp.push_back(pq.top()[2]);
            ans.push_back(temp);
            pq.pop();
        }
        
        return ans;
    }
};
```


