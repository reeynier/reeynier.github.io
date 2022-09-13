---
layout: post
title: "Elimination Game Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Recursion ]
similar: [ Recursion ]
featured: false
hidden: false
excerpt: LeetCode 390. You have a list arr of all integers in the range [1, n] sorted in a strictly increasing order. 

---

<br />

## Description

LeetCode Problem 390.

You have a list arr of all integers in the range [1, n] sorted in a strictly increasing order. Apply the following algorithm on arr:
* Starting from left to right, remove the first number and every other number afterward until you reach the end of the list.
* Repeat the previous step again, but this time from right to left, remove the rightmost number and every other number from the remaining numbers.
* Keep repeating the steps again, alternating left to right and right to left, until a single number remains.

Given the integer n, return the last number that remains in arr.

Example 1:
```
Input: n = 9
Output: 6
Explanation:
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
arr = [2, 4, 6, 8]
arr = [2, 6]
arr = [6]
```

Example 2:
```
Input: n = 1
Output: 1
```

Constraints:
* 1 <= n <= 10^9

<br />

## Sample C++ Code

Let n be how many numbers left in the array, and direction can be either left->right or right->left.

There are four cases to consider:
* n is odd and direction is left->right, [1, 2, 3, 4, 5] -> [2, 4], start of the sequence increases
* n is odd and direction is right->left, [1, 2, 3, 4, 5] -> [2, 4], start of the sequence increases
* n is even and direction is left->right, [1, 2, 3, 4] -> [2, 4], start of the sequence increases
* n is even and direction is right->left, [1, 2, 3, 4] -> [1, 3] , start of the sequence is the same as before

We also use diff to keep track of differences between adjacent integers left in the array. Every time we run the algorithm, we count if the start of the sequence increases or not, and if it increases, it increases by diff.

Example:
```
1 2 3 4 5 6 7 8 9 10 11 12 -> diff = 1
  2   4   6   8   10    12 -> start increases by 1, diff = 2
  2       6       10       -> start is the same, diff = 4
          6                -> start increases by 4, this is the Answer
```

```c
class Solution
{
public:
    int lastRemaining(int n)
    {
        int diff = 1, direction = 0, start = 1;
        //direction = 0 means direction is left->right
        //direction = 1 means direction is right->left
        while (n > 1)
        {
            if (n & 1 || direction == 0) {
            	// n is odd or when n is even and direction is left to right
            	// we increase start by diff
                start += diff;
            }
            // number of integers left in the array
            n /= 2;
            // diff is doubled 
            diff *= 2;         
            // flip direction     
            direction = !direction; 
        }
        return start;
    }
};
```


