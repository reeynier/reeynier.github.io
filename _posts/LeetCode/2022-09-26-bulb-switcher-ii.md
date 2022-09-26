---
layout: post
title: "Bulb Switcher II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Bit Manipulation, Depth-First Search, Breadth-First Search ]
similar: [ Bit Manipulation ]
featured: false
hidden: false
excerpt: LeetCode 672. There is a room with n bulbs labeled from 1 to n that all are turned on initially, and four buttons on the wall. 

---

<br />

## Description

LeetCode Problem 672.

There is a room with n bulbs labeled from 1 to n that all are turned on initially, and four buttons on the wall. Each of the four buttons has a different functionality where:
* Button 1: Flips the status of all the bulbs.
* Button 2: Flips the status of all the bulbs with even labels (i.e., 2, 4, ...).
* Button 3: Flips the status of all the bulbs with odd labels (i.e., 1, 3, ...).
* Button 4: Flips the status of all the bulbs with a label j = 3k + 1 where k = 0, 1, 2, ... (i.e., 1, 4, 7, 10, ...).

You must make exactly presses button presses in total. For each press, you may pick any of the four buttons to press.

Given the two integers n and presses, return the number of different possible statuses after performing all presses button presses.

Example 1:
```
Input: n = 1, presses = 1
Output: 2
Explanation: Status can be:
- [off] by pressing button 1
- [on] by pressing button 2
```

Example 2:
```
Input: n = 2, presses = 1
Output: 3
Explanation: Status can be:
- [off, off] by pressing button 1
- [on, off] by pressing button 2
- [off, on] by pressing button 3
```

Example 3:
```
Input: n = 3, presses = 1
Output: 4
Explanation: Status can be:
- [off, off, off] by pressing button 1
- [off, on, off] by pressing button 2
- [on, off, on] by pressing button 3
- [off, on, on] by pressing button 4
```

Example 4:
```
Input: n = 1, presses = 0
Output: 1
Explanation: Status can only be [on] since you cannot press any of the buttons.
```

Example 5:
```
Input: n = 1, presses = 2
Output: 2
Explanation: Status can be:
- [off] by pressing button 1 then button 1 again
- [on] by pressing button 1 then button 2
```

Constraints:
* 1 <= n <= 1000
* 0 <= presses <= 1000

<br />

## Sample C++ Code


```c
class Solution {
public:
    /**
    Observations:
    1) only the first 3 lights matter, since we can only switch (1) even (2) odd (3) (x = 1 MOD 3) lights
    2) all ops are commutative.
    3) there is only 8 states possible for all situations: All-on(111), 1(000), 2(010), 3(101), 4(011), 41(100), 42(110), 43(001)
    */
    int flipLights(int n, int p) {
    	// no presses, original state
        if (p == 0) return 1; 
        
        // constraint: (p > 0) : one light, binary states.
        if (n == 1) return 2; 

        // constraint: (p > 0 && n > 1) : one press, 
        // if (1) two lights -> all 2^2 but original state = 3 states 
        // (2) more than two lights -> 011, 010, 101, 000 = 4 states
        if (p == 1) return n > 2 ? 4 : 3; 

        // constraint: (p > 1 && n > 1) : two lights, multiple press, 4 states.
        if (n == 2) return 4; 

        // constraint: (p > 1 && n > 2) : if only two presses, 
        // can't be in 4(011) state -> 8-1 = 7
        return p == 2 ? 7 : 8; 
    }
};


```


