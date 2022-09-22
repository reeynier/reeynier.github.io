---
layout: post
title: "Construct The Rectangle Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 492. A web developer needs to know how to design a web page's size. So, given a specific rectangular web page's area, your job by now is to design a rectangular web page, whose length L and width W satisfy the following requirements

---

<br />

## Description

LeetCode Problem 492.

A web developer needs to know how to design a web page's size. So, given a specific rectangular web page's area, your job by now is to design a rectangular web page, whose length L and width W satisfy the following requirements:
* The area of the rectangular web page you designed must equal to the given target area.
* The width W should not be larger than the length L, which means L >= W.
* The difference between length L and width W should be as small as possible.

Return an array [L, W] where L and W are the length and width of theweb page you designed in sequence.

Example 1:
```
Input: area = 4
Output: [2,2]
Explanation: The target area is 4, and all the possible ways to construct it are [1,4], [2,2], [4,1]. 
But according to requirement 2, [1,4] is illegal; according to requirement 3,  [4,1] is not optimal compared to [2,2]. So the length L is 2, and the width W is 2.
```

Example 2:
```
Input: area = 37
Output: [37,1]
```

Example 3:
```
Input: area = 122122
Output: [427,286]
```

Constraints:
* 1 <= area <= 10^7

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<int> constructRectangle(int area) {
    	// The width is always less than or equal to the square root of the area, 
    	// so we start searching from sqrt(area) until we find the result.
        int a = sqrt(area);
        while (area % a) {
            a--;
        }
        return {area / a, a};
    }
};
```


