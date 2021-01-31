---
layout: post
title:  "Intersection Of Two Arrays Problem"
categories: [ Data Structure ]
tags: [ Hash Table, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 349. Given two arrays, write a function to compute their intersection.
---

<br />

## Description

LeetCode Problem 349. 

Given two arrays, write a function to compute their intersection.

Example 1:
```
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```

Example 2:
```
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
```

Note:

* Each element in the result must be unique.
* The result can be in any order.

<br />

## Solution

A straightforward approach is to use a `hash table`. We can use a hash table to store the elements appear in the two arrays. We iterate through the two arrays. If an element appears in the first array, we mark the value of that element in the hash table to be 0. If an element already appears in the first array, and also appears in the second array, we mark the value of that element in the hash table to be 1. For all elements that has a value to be 1 in the hash table will be outputed. By only using 0 and 1, we can avoid repitition of the elements in the final result.

The time complexity is O(n), and the space complexity is O(n). 


<br />


## Sample C++ Code

This is a C++ solution using the `hash table` approach. The time complexity is O(n), and the space complexity is O(n). 

```c
#include <iostream>
#include <vector>
#include <map>
#include <algorithm>

using namespace std;

vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
    map<int, int> ht;
    vector<int> ans;
    for (int i = 0; i < nums1.size(); i ++) {
        ht[nums1[i]] = 0;
    }
    for (int i = 0; i < nums2.size(); i ++) {
        if (ht.find(nums2[i]) != ht.end())
            ht[nums2[i]] = 1;
    }
    for (map<int, int>::iterator mit = ht.begin(); 
        mit != ht.end(); mit ++) {
        if (mit->second == 1)
            ans.push_back(mit->first);
    }
    return ans;
}

int main() {
    vector<int> nums1 = {1,2,2,1};
    vector<int> nums2 = {2,2};
    vector<int> res = intersection(nums1, nums2);
    for (int i = 0; i < res.size(); i ++) 
        cout << res[i] << " " << endl;
    return 0;
}
```


