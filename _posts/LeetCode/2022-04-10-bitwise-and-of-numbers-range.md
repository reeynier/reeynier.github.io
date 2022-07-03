---
layout: post
title: "Bitwise And Of Numbers Range Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Bit Manipulation ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 201. Given two integers left and right that represent the range [left, right], return the bitwise AND of all numbers in this range, inclusive.

---

<br />

## Description

LeetCode Problem 201.

Given two integers left and right that represent the range [left, right], return the bitwise AND of all numbers in this range, inclusive.

Example 1:
```
Input: left = 5, right = 7
Output: 4
```

Example 2:
```
Input: left = 0, right = 0
Output: 0
```

Example 3:
```
Input: left = 1, right = 2147483647
Output: 0
```

Constraints:
* 0 <= left <= right <= 2^31 - 1

<br />

## Sample C++ Code

Consider the case where range is given as [5,7]. The representation is given as following:
```
5 - 0101
6 - 0110
7 - 0111
```

Since we are dealing with and(&) operator, any presence of 0 with a 1 gives 0. We loop through the binary representation, and every time we consider the least significant bit. If n != m, then there are numbers between n and m, which means the and result of the last bit is 0.

Then we shift the binary representation right (n -> n>>1, m -> m>>1), until m and n are equal. For every right shift, the least significant bit will be 0, until m and n are equal. When they get equal, the result of and operation will be m (or n) after shifting.

```
5 < 7, so the fourth bit is 0.
5 -> 5>>1 = 2, 7 -> 7>>1 = 3.
2 < 3, so the third bit is 0.
2 -> 2>>1 = 1, 3 -> 3>>1 = 1.
1 == 1, so the first and second bit is 01.

So the final result is 0100 = 4.
```

```c
class Solution {
public:
    int rangeBitwiseAnd(int m, int n) {
        int count=0;
        // Loop till both numbers are equal
        while (m!=n) {   
            // right shift both numbers by 1
            m>>=1; 
            n>>=1;
            // increment the count
            count++;  
        }
        //count gives the number of zero places from the lsb so left shift m by count.
        return m<<count;
    }
};
```


