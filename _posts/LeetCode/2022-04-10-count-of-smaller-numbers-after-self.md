---
layout: post
title: "Count Of Smaller Numbers After Self Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search, Divide and Conquer, Binary Indexed Tree, Segment Tree, Merge Sort, Ordered Set ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 315. You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].

---

<br />

## Description

LeetCode Problem 315.

You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].

Example 1:
```
Input: nums = [5,2,6,1]
Output: [2,1,1,0]
Explanation:
To the right of 5 there are 2 smaller elements (2 and 1).
To the right of 2 there is only 1 smaller element (1).
To the right of 6 there is 1 smaller element (1).
To the right of 1 there is 0 smaller element.
```

Example 2:
```
Input: nums = [-1]
Output: [0]
```

Example 3:
```
Input: nums = [-1,-1]
Output: [0,0]
```

Constraints:
* 1 <= nums.length <= 10^5
* -10^4 <= nums[i] <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> countSmaller(vector<int>& nums) {
        vector<int> counts;
        vector<int> sorted;
        
        int len = nums.size();
        int left, right, mid, pos;
        
        if (len == 0)
            return counts;
        
        reverse(nums.begin(), nums.end());
        
        sorted.push_back(nums[0]);
        counts.push_back(0);
        
        for (int i = 1; i < len; i ++) {
            left = 0; 
            right = sorted.size();
            pos = left;
            while (left < right) {
                mid = (left + right) / 2;
                if (sorted[mid] < nums[i]) {
                    left = mid + 1;
                    pos = left;
                } else {
                    right = mid;
                    pos = right;
                }
            }
            sorted.insert(sorted.begin() + pos , nums[i]);
            counts.push_back(pos);
        }
        
        reverse(counts.begin(), counts.end());
        
        return counts;
        
    }
};
```


