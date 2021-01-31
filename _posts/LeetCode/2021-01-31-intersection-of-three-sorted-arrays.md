---
layout: post
title:  "Intersection Of Three Sorted Arrays Problem"
categories: [ Data Structure ]
tags: [ Hash Table, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 1213. Given three integer arrays arr1, arr2 and arr3 sorted in strictly increasing order, return a sorted array of only the integers that appeared in all three arrays.
---

<br />

## Description

LeetCode Problem 1213. 

Given three integer arrays arr1, arr2 and arr3 sorted in strictly increasing order, return a sorted array of only the integers that appeared in all three arrays.

 

Example 1:
```
Input: arr1 = [1,2,3,4,5], arr2 = [1,2,5,7,9], arr3 = [1,3,4,5,8]
Output: [1,5]
Explanation: Only 1 and 5 appeared in the three arrays.
```

Example 2:

```
Input: arr1 = [197,418,523,876,1356], arr2 = [501,880,1593,1710,1870], arr3 = [521,682,1337,1395,1764]
Output: []
```

<br />

## Solution

#### Hash Table Approach

A straightforward approach is to use a `hash table`. We can use a hash table to count the frequencies of each element in *arr1*, *arr2*, and *arr3*. Then we put the number that appear exactly 3 times to the result array. This is feasible because all of the three arrays are strictly increasing, so the elements will appear at most 3 times in all arrays.

The time complexity is O(n), and the space complexity is O(n). 

#### Three Pointer Approach

We can leverage the fact that the three arrays are strictly increasing to reduce the space complexity. 

We can use three pointers *p1*, *p2*, and *p3* to iterate through *arr1*, *arr2*, and *arr3*. During the iteration, we increment the pointer that points to the smallest number (*min(arr1[p1], arr2[p2], arr3[p3]*) forward. If the numbers pointed to by *p1*, *p2*, and *p3* are the same, we should put that number to the result array and move all three pointers forward.

The time complexity is O(n), and the space complexity is O(1). 

<br />


## Sample C++ Code

This is a C++ solution using a `hash table` approach. The time complexity is O(n), and the space complexity is O(n). 

```c
#include <iostream>
#include <vector>
#include <map>
#include <algorithm>

using namespace std;

vector<int> arraysIntersection(vector<int>& arr1, vector<int>& arr2, vector<int>& arr3) {
    unordered_map <int, int> ht;
    vector<int> res;
    for (int i = 0; i < arr1.size(); i++) {
        ht[arr1[i]] = 1;
    }
    for (int i = 0; i < arr2.size(); i++) {
        if (ht.find(arr2[i]) != ht.end()) {
            ht[arr2[i]]++;
        }
    }
    for (int i = 0; i < arr3.size(); i++) {
        if (ht.find(arr3[i]) != ht.end()) {
            ht[arr3[i]]++;
        }
        if (ht[arr3[i]] == 3) {
            res.push_back(arr3[i]);
        }
    }
    return res;
}

int main() {
    vector<int> arr1 = {1,2,3,4,5};
    vector<int> arr2 = {1,2,5,7,9};
    vector<int> arr3 = {1,3,4,5,8};
    vector<int> res = arraysIntersection(arr1, arr2, arr3);
    for (int i = 0; i < res.size(); i ++) 
        cout << res[i] << " " << endl;
    return 0;
}
```

This is a C++ solution using a `three pointer` approach. The time complexity is O(n), and the space complexity is O(1). 

```c
#include <iostream>
#include <vector>
#include <map>
#include <algorithm>

using namespace std;

vector<int> arraysIntersection(vector<int>& arr1, vector<int>& arr2, vector<int>& arr3) {
    vector<int> res;
    int p1 = 0, p2 = 0, p3 = 0;
    while(p1 < arr1.size() && p2 < arr2.size() && p3 < arr3.size()) {
        if ((arr1[p1] == arr2[p2]) && (arr1[p1] == arr3[p3])) {
            res.push_back(arr1[p1]);
            p1++; p2++; p3++;
            continue;
        }
        if ((arr1[p1] <= arr2[p2]) && (arr1[p1] <= arr3[p3]))
            p1++;
        else if ((arr2[p2] <= arr1[p1]) && (arr2[p2] <= arr3[p3]))
            p2++;
        else if ((arr3[p3] <= arr2[p2]) && (arr3[p3] <= arr1[p1]))
            p3++;
    }
    return res;
}

int main() {
    vector<int> arr1 = {1,2,3,4,5};
    vector<int> arr2 = {1,2,5,7,9};
    vector<int> arr3 = {1,3,4,5,8};
    vector<int> res = arraysIntersection(arr1, arr2, arr3);
    for (int i = 0; i < res.size(); i ++) 
        cout << res[i] << " " << endl;
    return 0;
}
```
