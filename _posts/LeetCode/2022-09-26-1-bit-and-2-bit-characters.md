---
layout: post
title: "1-Bit And 2-Bit Characters Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array ]
similar: [ Array ]
featured: false
hidden: false
excerpt: LeetCode 717. We have two special characters, the first character can be represented by one bit 0.

---

<br />

## Description

LeetCode Problem 717.

We have two special characters:
* The first character can be represented by one bit 0.
* The second character can be represented by two bits (10 or 11).

Given a binary array bits that ends with 0, return true if the last character must be a one-bit character.

Example 1:
```
Input: bits = [1,0,0]
Output: true
Explanation: The only way to decode it is two-bit character and one-bit character.
So the last character is one-bit character.
```

Example 2:
```
Input: bits = [1,1,1,0]
Output: false
Explanation: The only way to decode it is two-bit character and two-bit character.
So the last character is not one-bit character.
```

Constraints:
* 1 <= bits.length <= 1000
* bits[i] is either 0 or 1.

<br />

## Sample C++ Code


```c
class Solution {
public:
    bool isOneBitCharacter(vector<int>& bits) {
    	// The numbers of 1 between the last 0 and the second last 0 determine the answer.
        // If the number is odd, the answer is false.
        // If the number is even, the answer is true.
        int count_1 = 0;
        for (int i = (int) bits.size() - 2; i >= 0 && bits[i] == 1; i--) 
            count_1 ++;
        return (count_1 % 2 == 0);
    }
};
```


