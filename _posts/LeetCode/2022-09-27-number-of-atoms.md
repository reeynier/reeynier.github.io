---
layout: post
title: "Number Of Atoms Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Stack, Sorting ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 726. Given a string formula representing a chemical formula,return the count of each atom.

---

<br />

## Description

LeetCode Problem 726.

Given a string formula representing a chemical formula,return the count of each atom.

The atomic element always starts with an uppercase character, then zero or more lowercase letters, representing the name.

One or more digits representing that element's count may follow if the count is greater than 1. If the count is 1, no digits will follow.
* For example, "H2O" and "H2O2" are possible, but "H1O2" is impossible.
Two formulas are concatenated together to produce another formula.
* For example, "H2O2He3Mg4" is also a formula.
A formula placed in parentheses, and a count (optionally added) is also a formula.
* For example, "(H2O2)" and "(H2O2)3" are formulas.

Return the count of all elements as a string in the following form: the first name (in sorted order), followed by its count (if that count is more than 1), followed by the second name (in sorted order), followed by its count (if that count is more than 1), and so on.

Example 1:
```
Input: formula = "H2O"
Output: "H2O"
Explanation: The count of elements are {'H': 2, 'O': 1}.
```

Example 2:
```
Input: formula = "Mg(OH)2"
Output: "H2MgO2"
Explanation: The count of elements are {'H': 2, 'Mg': 1, 'O': 2}.
```

Example 3:
```
Input: formula = "K4(ON(SO3)2)2"
Output: "K4N2O14S4"
Explanation: The count of elements are {'K': 4, 'N': 2, 'O': 14, 'S': 4}.
```

Example 4:
```
Input: formula = "Be32"
Output: "Be32"
```

Constraints:
* 1 <= formula.length<= 1000
* formula consists of English letters, digits, '(', and ')'.
* formula is always valid.
* All the values in the output will fit in a 32-bit integer.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string countOfAtoms(string formula) {
        map<string, int> string_count;
        
        string lower = "", digit = "";
        
        vector<int> occ;
        occ.push_back(1);
        
        int n = formula.size();
        
        for (int i = n - 1; i >= 0; i--) {
            string element = formula[i] + lower;
            
            if (isdigit(formula[i])) {
                digit = formula[i] + digit;
            } else if (islower(formula[i])) {
                lower = formula[i] + lower;
            } else if (formula[i] == ')') {
                occ.push_back(occ.back() * (digit.empty() ? 1 : stoi(digit)));
                digit = "";
            } else if (formula[i] == '(') {
                occ.pop_back();
            } else {
                string_count[element] += occ.back() * (digit.empty() ? 1 : stoi(digit));
                lower = digit = "";
            }
        }
        
        string res = "";
        for (auto [elem, count] : string_count) {
            res += elem;
            if (count > 1) {
                res += to_string(count);
            }
        }
        
        return res;
    }
};
```


