---
layout: post
title:  "Kth Missing Positive Number Problem"
categories: [ Data Structure ]
tags: [ Hash Table, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 1539. Given an array arr of positive integers sorted in a strictly increasing order, and an integer k.
---

<br />

## Description

LeetCode Problem 1539. Given an array arr of positive integers sorted in a strictly increasing order, and an integer k.

Find the kth positive integer that is missing from this array.

 
Example 1:

```
Input: arr = [2,3,4,7,11], k = 5
Output: 9
Explanation: The missing positive integers are [1,5,6,8,9,10,12,13,...]. The 5th missing positive integer is 9.
```

Example 2:

```
Input: arr = [1,2,3,4], k = 2
Output: 6
Explanation: The missing positive integers are [5,6,7,...]. The 2nd missing positive integer is 6.
```

<br />

## Solution


We can scan through the array. During the scanning, we use a variable *i* to keep track of the index of array element. We use a variable *j* to keep track of how many positive numbers are missing. When *j* reaches *k*, we can stop scanning. We also use a variable *num* to enumerate all positive numbers, starting from 1 to the largest number in the array.

During the scanning, if *num* is in the array, which means *num = arr[i]*, we increase *i* to point to the next element in the array. If *num* is not in the array, we increase *j* which means one more positive number is missing in the array. We stop the search when *j* reaches *k*.


The time complexity is O(n), and the space complexity is O(1).


<br />

## Sample C++ Code


This is a C++ implementation of the above approach.

```c
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int findKthPositive(vector<int>& arr, int k) {
    int i = 0, j = 1, num = 0;
    while (j <= k) {
        num += 1;
        if ((i < arr.size()) && (num == arr[i])) {
            i ++;
        } else {
            j ++;
        }
    }
    return num;
}

int main() {
    vector<int> arr = {2, 3, 4, 7, 11};
    int k = 5;
    cout << findKthPositive(arr, k) << endl;
}
```
