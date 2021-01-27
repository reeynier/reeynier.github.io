---
layout: post
title:  "Jewels And Stones Problem"
categories: [ Data Structure ]
tags: [ Hash Table, Leetcode ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 771. You're given strings jewels representing the types of stones that are jewels, and stones representing the stones you have.
---

<br />

## Description

LeetCode Problem 771. You're given strings jewels representing the types of stones that are jewels, and stones representing the stones you have. Each character in stones is a type of stone you have. You want to know how many of the stones you have are also jewels.

Letters are case sensitive, so "a" is considered a different type of stone from "A". Jewels and stones consist of only English letters.

 

Example 1:

```
Input: jewels = "aA", stones = "aAAbbbb"
Output: 3
```

Example 2:

```
Input: jewels = "z", stones = "ZZ"
Output: 0
```

<br />

## Solution

When scanning through the jewels, we can use a hash table to store the jewels. Then for each stone, we check whether it matches any of the jewels.

To speed up the program, we can leverage the constraint that jewels and stones consist of only English letters. We can use an array instead of a hash table, and use the ASCII number of the letter as the index (instead of using the letter itself).

The time complexity is O(n + m), where n is the number of jewels and m is the number of stones. The space complexity is O(n).


<br />

## Sample C++ Code


This is a C++ implementation of the above approach.

```c
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

int numJewelsInStones(string J, string S) {
    vector<int> ht(100, 0);
    for (int i = 0; i < J.size(); i ++) {
        ht[J[i]-'A'] = 1;
    }
    int cnt = 0;
    for (int i = 0; i < S.size(); i ++) {
        if (ht[S[i]-'A'] == 1)
            cnt ++;
    }
    return cnt;
}

int main() {
    string J = "aA";
    string S = "aAAbbbb";
    cout << numJewelsInStones(J, S) << endl;
}
```
