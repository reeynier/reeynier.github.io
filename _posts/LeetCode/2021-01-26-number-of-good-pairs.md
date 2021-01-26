---
layout: post
title:  "Number Of Good Pairs Problem"
categories: [ Data Structure ]
tags: [ Hash Table, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 1512. Given an array of integers nums. Return the number of good pairs.
---

<br />

## Description

LeetCode Problem 1512. Given an array of integers nums. A pair (i,j) is called good if nums[i] == nums[j] and i < j.

Return the number of good pairs.

 

Example 1:

```
Input: nums = [1,2,3,1,1,3]
Output: 4
Explanation: There are 4 good pairs (0,3), (0,4), (3,4), (2,5) 0-indexed.
```

Example 2:

```
Input: nums = [1,1,1,1]
Output: 6
Explanation: Each pair in the array are good.
```

Example 3:

```
Input: nums = [1,2,3]
Output: 0
```

<br />

## Solution


We can scan through the array. During the scanning, we use a hash table to store the number of occurrences of each unique integer. For example, for the array [1, 2, 3, 1, 1, 3], we have: (1, 3), (2, 1), (3, 2). The first number, which is the key of the hash table, shows the integer in the array. The second number shows how many times this integer appears in the array.

Then we can scan through the hash table, and the number of good pairs is *(n - 1) \* n / 2* (n is the number of occurrences of each integer). Finally, we add up all the number of good pairs and return the result.





The time complexity is O(n), and the space complexity is O(n).


<br />

## Sample C++ Code


This is a C++ implementation of the above approach.

```c
#include <iostream>
#include <vector>
#include <map>
#include <algorithm>

using namespace std;

int numIdenticalPairs(vector<int>& nums) {
    map<int, int> ht;
    for (int i = 0; i < nums.size(); i ++) {
        if (ht.find(nums[i]) == ht.end())
            ht[nums[i]] = 0;
        ht[nums[i]] ++;
    }
    int cnt = 0;
    for (map<int, int>::iterator mit = ht.begin(); 
        mit != ht.end(); mit ++) {
        int n = mit->second;
        cnt += (n - 1) * n / 2;
    }
    return cnt;
}

int main() {
    vector<int> nums = {1, 2, 3, 1, 1, 3};
    cout << numIdenticalPairs(nums) << endl;
}
```
