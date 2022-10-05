---
layout: post
title: "Prime Number Of Set Bits In Binary Representation Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Bit Manipulation ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 762. Given two integers left and right, return the count of numbers in the inclusive range [left, right] having a prime number of set bits in their binary representation.

---

<br />

## Description

LeetCode Problem 762.

Given two integers left and right, return the count of numbers in the inclusive range [left, right] having a prime number of set bits in their binary representation.

Recall that the number of set bits an integer has is the number of 1's present when written in binary.
* For example, 21 written in binary is 10101, which has 3 set bits.

Example 1:
```
Input: left = 6, right = 10
Output: 4
Explanation:
6  -> 110 (2 set bits, 2 is prime)
7  -> 111 (3 set bits, 3 is prime)
8  -> 1000 (1 set bit, 1 is not prime)
9  -> 1001 (2 set bits, 2 is prime)
10 -> 1010 (2 set bits, 2 is prime)
4 numbers have a prime number of set bits.
```

Example 2:
```
Input: left = 10, right = 15
Output: 5
Explanation:
10 -> 1010 (2 set bits, 2 is prime)
11 -> 1011 (3 set bits, 3 is prime)
12 -> 1100 (2 set bits, 2 is prime)
13 -> 1101 (3 set bits, 3 is prime)
14 -> 1110 (3 set bits, 3 is prime)
15 -> 1111 (4 set bits, 4 is not prime)
5 numbers have a prime number of set bits.
```

Constraints:
* 1 <= left <= right <= 10^6
* 0 <= right - left <= 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int countPrimeSetBits(int L, int R) {
        int count=0;
        for (int i = L; i <= R; i++) {
            if (checkPrime(findSetBits(i))) 
                count++;
        }
        return count;
    }
    int findSetBits(int n) {
        int count = 0;
        while (n) {
            n = n & (n - 1);
            count ++;
        }
        return count;
    }
    bool checkPrime(int x) {
        return (x == 2 || x == 3 || x == 5 || x == 7 ||
                x == 11 || x == 13 || x == 17 || x == 19);
    }
};
```

