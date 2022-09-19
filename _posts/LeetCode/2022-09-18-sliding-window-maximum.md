---
layout: post
title: "Sliding Window Maximum Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Queue, Sliding Window, Heap, Monotonic Queue ]
similar: [ Sliding Window ]
featured: false
hidden: false
excerpt: LeetCode 239. You are given an array of integersnums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

---

<br />

## Description

LeetCode Problem 239.

You are given an array of integersnums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

Example 1:
```
Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
1 [3  -1  -3] 5  3  6  7       3
1  3 [-1  -3  5] 3  6  7       5
1  3  -1 [-3  5  3] 6  7       5
1  3  -1  -3 [5  3  6] 7       6
1  3  -1  -3  5 [3  6  7]      7
```

Example 2:
```
Input: nums = [1], k = 1
Output: [1]
```

Example 3:
```
Input: nums = [1,-1], k = 1
Output: [1,-1]
```

Example 4:
```
Input: nums = [9,11], k = 2
Output: [11]
```

Example 5:
```
Input: nums = [4,-2], k = 2
Output: [4]
```

Constraints:
* 1 <= nums.length <= 10^5
* -10^4 <= nums[i] <= 10^4
* 1 <= k <= nums.length

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        int len = nums.size();
        vector<int> ans;
        deque<int> maxs;
        
        
        for (int i = 0; i < len; i ++) {
            while (!maxs.empty() && maxs.back() < nums[i]) maxs.pop_back();
            maxs.push_back(nums[i]);

            if (i >= k && nums[i-k] == maxs.front())
                maxs.pop_front();
            if (i >= k - 1)
                ans.push_back(maxs.front());
        }
        
        return ans;
    }
};
```


