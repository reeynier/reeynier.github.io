---
layout: post
title:  "Longest Continuous Subarray With Absolute Diff Less Than Or Equal To Limit Problem"
categories: [ Algorithm ]
tags: [ Sliding Window, Queue, Leetcode ]
similar: [ Sliding Window ]
featured: false
hidden: false
excerpt: LeetCode 1438. Given an array of integers **nums** and an integer **limit**, return the size of the longest non-empty subarray such that the absolute difference between any two elements of this subarray is less than or equal to **limit**. 
---

<br />

## Description

LeetCode Problem 1438. Given an array of integers **nums** and an integer **limit**, return the size of the longest non-empty subarray such that the absolute difference between any two elements of this subarray is less than or equal to **limit**. 

Example: 
```
Input: nums = [8,2,4,7], limit = 4
Output: 2 
Explanation: All subarrays are: 
[8] with maximum absolute diff |8-8| = 0 <= 4.
[8,2] with maximum absolute diff |8-2| = 6 > 4. 
[8,2,4] with maximum absolute diff |8-2| = 6 > 4.
[8,2,4,7] with maximum absolute diff |8-2| = 6 > 4.
[2] with maximum absolute diff |2-2| = 0 <= 4.
[2,4] with maximum absolute diff |2-4| = 2 <= 4.
[2,4,7] with maximum absolute diff |2-7| = 5 > 4.
[4] with maximum absolute diff |4-4| = 0 <= 4.
[4,7] with maximum absolute diff |4-7| = 3 <= 4.
[7] with maximum absolute diff |7-7| = 0 <= 4. 
Therefore, the size of the longest subarray is 2.

Input: nums = [10,1,2,4,7,2], limit = 5
Output: 4 
Explanation: The subarray [2,4,7,2] is the longest since the maximum absolute diff is |2-7| = 5 <= 5.
```

<br />

## Solution

#### Brute Force Approach

A simple solution is to use the `brute force` approach. 

We use two pointers *l* and *r*. For the left pointer, we iterate *l* through the array. For the right pointer, we iterate *r* from *l+1* to the end of the array. The numbers between the two pointers (inclusive) form a subarray of the array. We can iterate through the numbers in the subarray, find out the max and min numbers, and check whether the absolute difference is less than or equal to *limit*. This gives us an approach of time complexity of O(n<sup>3</sup>) and space complexity of O(1).

#### Optimization 1

We can do a little optimization here. When we iterate the right pointer *r* from *l+1* to the end of the array, we keep track of the max and min numbers between *l* and *r* (inclusive). If the new *r* is larger than max, we update max; if the new *r* is smaller than min, we update min. Then we check if the absolute difference between min and max is less than or equal to *limit*. This optimization reduces the time complexity to O(n<sup>2</sup>). The space complexity is O(1).


#### Optimization 2


We can further reduce the time complexity. Note that during the iteration, each time we increase the left pointer by 1. There are repetitive calculation here. 

If the next number is neither the min nor the max number in the subarray, the difference between min and max of the new subarray will be the same. We do not need to calculate the min-max difference again. Thus, when we move the left pointer, we can directly move it to the location of the min or max number. Note that this time, we do not wait until the right pointer to finish scanning the rest of the array, to move the left pointer. We move the left pointer when the min-max difference is larger than the limit. 


#### Queue Approach

Another approach is to use queues. We use two queues (a min queue and a max queue) to keep track of the min and max values so far. 

Again, we use two pointers *i* and *j* to represent subarrays. We use *j* to iterate through all the numbers in the array. The pointer *i* starts from the 0th number in the array. 

If *nums[j]* is larger than the last number in the max queue, we pop the last number of the max queue. We repeat this step until the max queue is empty or the last number is larger or equal to *nums[j]*. We do the same thing for the min queue. The difference is to pop up the last number in the min queue if *nums[j]* is less than the last number.

Then we push *nums[j]* to the max queue and the min queue. All the numbers in the max queue is larger than or equal to the numbers after it. All the numbers in the min queue is smaller than or equal to the numbers after it. Now, the front number of the max queue is the max number between *i* and *j* (inclusive). The front number of the min queue is the min number between *i* and *j* (inclusive).

Then, we move the pointer *i* until the absolute difference between the front numbers of min queue and max queue is less than or equal to the limit.

The time complexity of this approach is O(nlogn).




<br />

## Sample C++ Code

Below is a C++ implementation of the optimization 2 approach.
```c
#include <iostream>
#include <queue>
#include <algorithm>

using namespace std;

int longestSubarray(vector<int>& nums, int limit) {
    int len = nums.size();

    int maxsub = 0;
    int i = 0, j = 0;
    int minNum, maxNum;
    int minIdx = 0, maxIdx = 0;
    while (i < len) {
        minNum = nums[i], maxNum = nums[i];
        minIdx = i, maxIdx = i;
        for (j = i + 1; j < len; j ++) {
            if (nums[j] < minNum) {
                minNum = nums[j];
                minIdx = j;
            }
            if (nums[j] > maxNum) {
                maxNum = nums[j];
                maxIdx = j;
            }
            if (abs(minNum - maxNum) > limit)
                break;
        }
        j --;
        if (maxsub < j - i + 1) {
            maxsub = j - i + 1;
        }
        i = min(minIdx, maxIdx) + 1;
    }
    return maxsub;
}

int main() {
    vector<int> nums={10, 1, 2, 4, 7, 2};
    int limit = 5;
    cout << longestSubarray(nums, limit) << endl;
}
```


This is a C++ implementation of the queue approach.

```c
#include <iostream>
#include <queue>
#include <algorithm>

using namespace std;

int longestSubarray(vector<int>& nums, int limit) {
    int len = nums.size();
    
    deque<int> maxs;
    deque<int> mins;
    
    int maxsub = 0;
    int i = 0;
    for (int j = 0; j < len; j ++) {
        while (!maxs.empty() && nums[j] > maxs.back()) maxs.pop_back();
        while (!mins.empty() && nums[j] < mins.back()) mins.pop_back();
        
        maxs.push_back(nums[j]);
        mins.push_back(nums[j]);
        
        while (maxs.front() - mins.front() > limit) {
            if (maxs.front() == nums[i])
                maxs.pop_front();
            if (mins.front() == nums[i])
                mins.pop_front();
            i ++;
        }
        maxsub = max(maxsub, j - i + 1);
    }
    return maxsub;
}

int main() {
    vector<int> nums={10, 1, 2, 4, 7, 2};
    int limit = 5;
    cout << longestSubarray(nums, limit) << endl;
}
```
