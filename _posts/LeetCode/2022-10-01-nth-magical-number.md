---
layout: post
title: "Nth Magical Number Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Math, Binary Search ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 878. A positive integer is magical if it is divisible by either a or b.

---

<br />

## Description

LeetCode Problem 878.

A positive integer is magical if it is divisible by either a or b.

Given the three integers n, a, and b, return the n^th magical number. Since the answer may be very large, return it modulo 10^9 + 7.

Example 1:
```
Input: n = 1, a = 2, b = 3
Output: 2
```

Example 2:
```
Input: n = 4, a = 2, b = 3
Output: 6
```

Example 3:
```
Input: n = 5, a = 2, b = 4
Output: 10
```

Example 4:
```
Input: n = 3, a = 6, b = 4
Output: 8
```

Constraints:
* 1 <= n <= 10^9
* 2 <= a, b <= 4 * 10^4

<br />

## Sample C++ Code


```c
class Solution {
public:
    int MOD = 1000000007;
    int nthMagicalNumber(int n, int a, int b) {
        // Left limit to start finding the nth magica number
        long long l = 0; 
       
        // Right limit, the nth magic number will stay within r
        long long r = (long long)min(a,b)*n; 
	   
        while (l <= r) {
            long long mid = l + (r - l) / 2;

            // divs is the number of magical numbers till mid that will be equal to 
            // numbes divisible by a + numbers divisble by b - numbers divisible by both 
            int divs = mid/a + mid/b - mid/lcm(a,b); 
            
            //If we find that there are n magical numbers till mid, 
            // we need to look for the nth magical number itself
            if (divs == n) { 
                if (mid % a == 0 || mid % b == 0) {  
                    //It is possible that mid is that number
                    return mid % MOD;
                } else { 
                    //If not, its some number before mid
                    r = mid-1;
                }
            } else { 
                // Reduce search space based on number of magical numbers till mid
                if (divs < n) {
                    l = mid + 1;
                } else {
                    r = mid - 1;
                }
            }
        }
        
        return l % MOD; 
    }
};
```


