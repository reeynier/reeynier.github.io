---
layout: post
title: "Count Primes Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, Enumeration, Number Theory ]
similar: [ Math ]
featured: false
hidden: false
excerpt: LeetCode 204. Given an integer n, return the number of prime numbers that are strictly less than n.

---

<br />

## Description

LeetCode Problem 204.

Given an integer n, return the number of prime numbers that are strictly less than n.

Example 1:
```
Input: n = 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```

Example 2:
```
Input: n = 0
Output: 0
```

Example 3:
```
Input: n = 1
Output: 0
```

Constraints:
* 0 <= n <= 5 * 10^6

<br />

## Sample C++ Code


```c
class Solution {
public:
	int countPrimes(int n) {
		vector<bool> prime(n + 1, true);
		prime[0] = false;
		prime[1] = false;
		for (int i = 2; i * i <= n; i++) {
			if (prime[i]) {
				for (int j = i * i; j <= n; j += i) {
					prime[j] = false;
				}
			}
		}
		
		//counting prime numbers
		int primeCount = 0;
		for (int i = 2; i < n; i++) {
			if (prime[i]) {
				primeCount++;
			}
		}
		return primeCount;
	}
};
```


