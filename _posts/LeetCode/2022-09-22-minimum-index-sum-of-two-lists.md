---
layout: post
title: "Minimum Index Sum Of Two Lists Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, String ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 599. Suppose Andy and Doris want to choose a restaurant for dinner, and they both have a list of favorite restaurants represented by strings.

---

<br />

## Description

LeetCode Problem 599.

Suppose Andy and Doris want to choose a restaurant for dinner, and they both have a list of favorite restaurants represented by strings.

You need to help them find out their common interest with the least list index sum. If there is a choice tie between answers, output all of them with no order requirement. You could assume there always exists an answer.

Example 1:
```
Input: list1 = ["Shogun","Tapioca Express","Burger King","KFC"], list2 = ["Piatti","The Grill at Torrey Pines","Hungry Hunter Steakhouse","Shogun"]
Output: ["Shogun"]
Explanation: The only restaurant they both like is "Shogun".
```

Example 2:
```
Input: list1 = ["Shogun","Tapioca Express","Burger King","KFC"], list2 = ["KFC","Shogun","Burger King"]
Output: ["Shogun"]
Explanation: The restaurant they both like and have the least index sum is "Shogun" with index sum 1 (0+1).
```

Example 3:
```
Input: list1 = ["Shogun","Tapioca Express","Burger King","KFC"], list2 = ["KFC","Burger King","Tapioca Express","Shogun"]
Output: ["KFC","Burger King","Tapioca Express","Shogun"]
```

Example 4:
```
Input: list1 = ["Shogun","Tapioca Express","Burger King","KFC"], list2 = ["KNN","KFC","Burger King","Tapioca Express","Shogun"]
Output: ["KFC","Burger King","Tapioca Express","Shogun"]
```

Example 5:
```
Input: list1 = ["KFC"], list2 = ["KFC"]
Output: ["KFC"]
```

Constraints:
* 1 <= list1.length, list2.length <= 1000
* 1 <= list1[i].length, list2[i].length <= 30
* list1[i] and list2[i] consist of spaces ' ' and English letters.
* All the stings of list1 are unique.
* All the stings of list2are unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    vector<string> findRestaurant(vector<string>& list1, vector<string>& list2) {
        vector<string> res;
        unordered_map<string,int> m;
        int min = INT_MAX;
        for (int i = 0; i < list1.size(); i++) 
            m[list1[i]] = i;
        for (int i = 0; i < list2.size(); i++)
            if (m.count(list2[i]) != 0) {
                if (m[list2[i]] + i < min) {
                    min = m[list2[i]] + i; 
                    res.clear(); 
                    res.push_back(list2[i]);
                }
                else if(m[list2[i]] + i == min) {
                    res.push_back(list2[i]);
                }
            }
        return res;
    }
};
```


