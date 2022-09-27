---
layout: post
title: "Find Smallest Letter Greater Than Target Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Binary Search ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 744. Given a characters array letters that is sorted in non-decreasing order and a character target, return the smallest character in the array that is larger than target.

---

<br />

## Description

LeetCode Problem 744.

Given a characters array letters that is sorted in non-decreasing order and a character target, return the smallest character in the array that is larger than target.

Note that the letters wrap around.
* For example, if target == 'z' and letters == ['a', 'b'], the answer is 'a'.

Example 1:
```
Input: letters = ["c","f","j"], target = "a"
Output: "c"
```

Example 2:
```
Input: letters = ["c","f","j"], target = "c"
Output: "f"
```

Example 3:
```
Input: letters = ["c","f","j"], target = "d"
Output: "f"
```

Example 4:
```
Input: letters = ["c","f","j"], target = "g"
Output: "j"
```

Example 5:
```
Input: letters = ["c","f","j"], target = "j"
Output: "c"
```

Constraints:
* 2 <= letters.length <= 10^4
* letters[i] is a lowercase English letter.
* letters is sorted in non-decreasing order.
* letters contains at least two different characters.
* target is a lowercase English letter.

<br />

## Sample C++ Code


```c
class Solution {
public:
    char nextGreatestLetter(vector<char>& letters, char target) {
        int low = 0;
        int high = letters.size()-1;
        
        while (low < high) {
            int mid = low + (high - low) / 2;
            if (letters[mid] <= target) {
                low = mid + 1;
            } else {
                high = mid;
            }
        }
        
        return letters[low] > target ? letters[low] : letters[0];
    }
};
```


