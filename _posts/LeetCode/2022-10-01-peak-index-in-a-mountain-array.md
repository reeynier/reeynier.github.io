---
layout: post
title: "Peak Index In A Mountain Array Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 852. Let's call an array arr a mountainif the following properties hold

---

<br />

## Description

LeetCode Problem 852.

Let's call an array arr a mountainif the following properties hold:
* arr.length >= 3
* There exists some i with0 < i< arr.length - 1such that:
* arr[0] < arr[1] < ... arr[i-1] < arr[i] 
* arr[i] > arr[i+1] > ... > arr[arr.length - 1]

Given an integer array arr that is guaranteed to bea mountain, return anyisuch thatarr[0] < arr[1] < ... arr[i - 1] < arr[i] > arr[i + 1] > ... > arr[arr.length - 1].

Example 1:
```
Input: arr = [0,1,0]
Output: 1
```

Example 2:
```
Input: arr = [0,2,1,0]
Output: 1
```

Example 3:
```
Input: arr = [0,10,5,2]
Output: 1
```

Example 4:
```
Input: arr = [3,4,5,1]
Output: 2
```

Example 5:
```
Input: arr = [24,69,100,99,79,78,67,36,26,19]
Output: 2
```

Constraints:
* 3 <= arr.length <= 10^4
* 0 <= arr[i] <= 10^6
* arr is guaranteed to be a mountain array.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int peakIndexInMountainArray(vector<int>& arr) {
        int low = 0, high = arr.size()-1;
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (arr[mid] < arr[mid+1])
                low = mid + 1;
            else
                high = mid - 1;
        }
        return low;
    }
};
```


