---
layout: post
title: "Fraction To Recurring Decimal Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, Math, String ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 166. Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

---

<br />

## Description

LeetCode Problem 166.

Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

If multiple answers are possible, return any of them.

It is guaranteed that the length of the answer string is less than 10^4 for all the given inputs.

Example 1:
```
Input: numerator = 1, denominator = 2
Output: "0.5"
```

Example 2:
```
Input: numerator = 2, denominator = 1
Output: "2"
```

Example 3:
```
Input: numerator = 2, denominator = 3
Output: "0.(6)"
```

Example 4:
```
Input: numerator = 4, denominator = 333
Output: "0.(012)"
```

Example 5:
```
Input: numerator = 1, denominator = 5
Output: "0.2"
```

Constraints:
* -2^31 <=numerator, denominator <= 2^31 - 1
* denominator != 0

<br />

## Sample C++ Code


```c
string fractionToDecimal(int numerator, int denominator) {
	if (!numerator) {
		return "0";
	}

	string result;
	long long remainder = numerator;
	unordered_map<long long, int> pattern;

	// Determine sign so that we don't have to care about it later.
	if ((remainder < 0 && denominator > 0) ||
		(remainder > 0 && denominator < 0)) {
		result += "-";
	}

	while (remainder) {
		result += to_string(llabs(remainder / denominator));
		remainder = remainder % denominator;

		// Each time we got a new remainder, check if it matches a repeat pattern. 
		if (pattern.find(remainder) != pattern.end()) {
			result.insert(pattern[remainder], "(");
			result.append(")");
			break;
		}

		// If we are not done by dividing once, we need a ".".
		if (remainder && result.find('.') == result.npos) {
			result += ".";
		}

		// Save the remainder and its correspounding position in the result.
		pattern[remainder] = result.length();

		remainder *= 10;
	}

	return result;
}
```


