---
layout: post
title: "Broken Calculator Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Greedy ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 991. There is a broken calculator that has the integer startValue on its display initially. 

---

<br />

## Description

LeetCode Problem 991.

There is a broken calculator that has the integer startValue on its display initially. In one operation, you can:
* multiply the number on display by 2, or
* subtract 1 from the number on display.

Given two integers startValue and target, return the minimum number of operations needed to display target on the calculator.

Example 1:
```
Input: startValue = 2, target = 3
Output: 2
Explanation: Use double operation and then decrement operation {2 -> 4 -> 3}.
```

Example 2:
```
Input: startValue = 5, target = 8
Output: 2
Explanation: Use decrement and then double {5 -> 4 -> 8}.
```

Example 3:
```
Input: startValue = 3, target = 10
Output: 3
Explanation: Use double, decrement and double {3 -> 6 -> 5 -> 10}.
```

Example 4:
```
Input: startValue = 1024, target = 1
Output: 1023
Explanation: Use decrement operations 1023 times.
```

Constraints:
* 1 <= x, y <= 10^9

<br />

## Sample C++ Code


```c
class Solution {
public:
    // 1. reduce target value as much as possible  
    // because this question can be done by greedy
    // 2. if divisible by 2 divide by 2  
    // 3. else increase by 1
    // 4. if target becomes less than startValue then only option left is to increasse
    int brokenCalc(int startValue, int target) {
        long long ans = 0;
        long long tar = target;
        while (startValue != tar) {
            if (tar % 2 == 0 and startValue < tar) {
                tar /= 2;
            }
            else if (tar > startValue) {
                tar += 1;
            }
            else{
                ans += abs(tar - startValue) - 1;
                tar = startValue;
            }
            ans++;
        }
        return ans;
    }
};
```


