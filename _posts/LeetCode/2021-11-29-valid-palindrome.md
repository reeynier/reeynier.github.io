---
layout: post
title: "Valid Palindrome Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Two Pointers, String ]
similar: [ Two Pointers ]
featured: false
hidden: false
excerpt: LeetCode 125. A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.
---

<br />

## Description

LeetCode Problem 125.

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

Example 1:
```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

Example 2:
```
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

Example 3:
```
Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.
```

Constraints:
* 1 <= s.length <= 2 * 10^5
* s consists only of printable ASCII characters.

<br />

## Sample C++ Code


```c
bool isPalindrome(string s) {
    for (int i = 0, j = s.size() - 1; i < j; i++, j--) { 
    	// Move 2 pointers from each end until they collide
        while (!isalnum(s[i]) && i < j) 
        	// Increment left pointer if not alphanumeric
        	i++; 
        while (!isalnum(s[j]) == false && i < j) 
        	// Decrement right pointer if no alphanumeric
        	j--; 
        if (toupper(s[i]) != toupper(s[j])) 
        	// Exit and return error if not match
        	return false; 
    }
    
    return true;
}
```


