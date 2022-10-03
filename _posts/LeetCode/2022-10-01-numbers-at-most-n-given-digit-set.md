---
layout: post
title: "Numbers At Most N Given Digit Set Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Math, String, Binary Search, Dynamic Programming ]
similar: [ Binary Search ]
featured: false
hidden: false
excerpt: LeetCode 902. Given an array of digits which is sorted in non-decreasing order. You can write numbers using each digits[i] as many times as we want. For example, if digits = ['1','3','5'], we may write numbers such as '13', '551', and '1351315'.

---

<br />

## Description

LeetCode Problem 902.

Given an array of digits which is sorted in non-decreasing order. You can write numbers using each digits[i] as many times as we want. For example, if digits = ['1','3','5'], we may write numbers such as '13', '551', and '1351315'.

Return the number of positive integers that can be generated that are less than or equal to a given integer n.

Example 1:
```
Input: digits = ["1","3","5","7"], n = 100
Output: 20
Explanation: 
The 20 numbers that can be written are:
1, 3, 5, 7, 11, 13, 15, 17, 31, 33, 35, 37, 51, 53, 55, 57, 71, 73, 75, 77.
```

Example 2:
```
Input: digits = ["1","4","9"], n = 1000000000
Output: 29523
Explanation: 
We can write 3 one digit numbers, 9 two digit numbers, 27 three digit numbers,
81 four digit numbers, 243 five digit numbers, 729 six digit numbers,
2187 seven digit numbers, 6561 eight digit numbers, and 19683 nine digit numbers.
In total, this is 29523 integers that can be written using the digits array.
```

Example 3:
```
Input: digits = ["7"], n = 8
Output: 1
```

Constraints:
* 1 <= digits.length <= 9
* digits[i].length == 1
* digits[i] is a digit from '1' to '9'.
* All the values in digits are unique.
* digits is sorted in non-decreasing order.
* 1 <= n <= 10^9

<br />

## Sample C++ Code with and without Comments


```c
class Solution {
public:
    int atMostNGivenDigitSet(vector<string>& D, int N) {
        string NS = to_string(N);
        int nsize = NS.size(), dsize = D.size(), rtn = 0;
        
        for (int i = 1 ; i < nsize ; ++i)
            // Since all digits are unique, for i-digit numbers, 
            // we have dsize^i count of numbers.
            // For example, D=[1,2,3], N=23100, dsize=3, nsize=5
            // we have 3^1 1-digit number, 3^2 2-digt number, 
            // 3^3 3-digt number, 3^4 4-digit number. 
            rtn += pow(dsize, i);
        
        for (int i = 0 ; i < nsize ; ++i) {
            // This loop handles the nsize-digit numbers from left to right digit.
            bool hasSameNum = false;
            for (string &d : D) {
                if (d[0] < NS[i]) 
                    // If d[0] < NS[i], continue with the above example, 
                    // when d[0]=1, i=0, NS[i]=2,
                    // for 1xxxx, there are 3^4 count of 4-digit numbers.
                    // When d[0]=1 or 2, i=1, NS=3, ie 21xxx and 22xxx,
                    // there are 3^3 and 3^3 count of 3-digit numbers.
                    rtn += pow(dsize, nsize - i - 1);
                else if (d[0] == NS[i]) 
                    // If d[0] == NS[i], for example when d[0]=2, i=0, NS[i]=2
                    // for 2xxxx, we do not increase the counts.
                    // This is because we will count the numbers between 20000 and 23100 later.
                    // When d[0]=1 or 2, i=1, NS=3, ie 21xxx and 22xxx, 
                    // they will be counted in the (d[0] < NS[i]) condition
                    // When d[0]=3, i=1, NS=3, ie 23xxx (23000-23100), they will be counted in next iterations.
                    // When d[0]=1, i=2, NS=1, ie 231xx (23100-23100), they will be counted in next iterations.
                    hasSameNum = true;
                // If d[0] > NS[i], eg d[0]=3, NS[i]=2, for 3xxxx, 
                // we do not increase the counts, because it is larger than N.
            }
            if (!hasSameNum) 
                // For the ith digit, it doesn't match with any elements in D,
                // it means d[0]==NS[i] was never true in this digt.
                // then all the numbers that can be formed by elements in D 
                // and less than N have been counted, we can return the current count.
                return rtn;
        }
        // For every digit of N, it can be composed from elements in D, 
        // (because for each iteration, hasSameNum is always true),
        // so we add N itself to the answer (rtn+1)
        return rtn+1;
    }
};
```

```c
class Solution {
public:
    int atMostNGivenDigitSet(vector<string>& D, int N) {
        string NS = to_string(N);
        int nsize = NS.size(), dsize = D.size(), rtn = 0;
        
        for (int i = 1 ; i < nsize ; ++i) 
            rtn += pow(dsize, i);
        
        for (int i = 0 ; i < nsize ; ++i) {
            bool hasSameNum = false;
            for (string &d : D) {
                if (d[0] < NS[i]) 
                    rtn += pow(dsize, nsize - i - 1);
                else if (d[0] == NS[i]) 
                    hasSameNum = true;
            }
            if (!hasSameNum) 
                return rtn;
        }
        return rtn+1;
    }
};
```


