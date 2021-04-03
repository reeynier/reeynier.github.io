---
layout: post
title:  "Determine Color Of A Chessboard Square Problem"
categories: [ Data Structure ]
tags: [ String, Leetcode ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 1812. You are given coordinates, a string that represents the coordinates of a square of the chessboard. 
---

<br />

## Description

LeetCode Problem 1812. 

You are given coordinates, a string that represents the coordinates of a square of the chessboard. Below is a chessboard for your reference.

```
8 w b w b w b w b 
7 b w b w b w b w
6 w b w b w b w b 
5 b w b w b w b w
4 w b w b w b w b 
3 b w b w b w b w
2 w b w b w b w b 
1 b w b w b w b w
  a b c d e f g h
```
(Note: "b" stands for black square, and "w" stands for white square.)

Return true if the square is white, and false if the square is black.

The coordinate will always represent a valid chessboard square. The coordinate will always have the letter first, and the number second.

 

Example 1:
```
Input: coordinates = "a1"
Output: false
Explanation: From the chessboard above, the square with coordinates "a1" is black, so return false.
```

Example 2:
```
Input: coordinates = "h3"
Output: true
Explanation: From the chessboard above, the square with coordinates "h3" is white, so return true.
```

Example 3:
```
Input: coordinates = "c7"
Output: false
```

Constraints:
* coordinates.length == 2
* 'a' <= coordinates[0] <= 'h'
* '1' <= coordinates[1] <= '8'

<br />

## Sample C++ Code


This is a C++ solution.

```c
class Solution {
public:
    bool squareIsWhite(string coordinates) {
        char t = coordinates[0];
        char s = coordinates[1];
        if(t == 'a' || t == 'c' || t == 'e' || t == 'g')
        {
            if((s - '0') % 2 == 1) return false;
            else return true;    
        }
        else
        {
            if((s - '0') % 2 == 0) return false;
            else return true;
        }
    }
};
```
