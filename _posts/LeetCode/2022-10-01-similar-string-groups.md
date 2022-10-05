---
layout: post
title: "Similar String Groups Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, String, Depth-First Search, Breadth-First Search, Union Find ]
similar: [ Depth-First Search ]
featured: false
hidden: false
excerpt: LeetCode 839. Two strings Xand Yare similar if we can swap two letters (in different positions) of X, so thatit equals Y. Also two strings X and Y are similar if they are equal.

---

<br />

## Description

LeetCode Problem 839.

Two strings Xand Yare similar if we can swap two letters (in different positions) of X, so thatit equals Y. Also two strings X and Y are similar if they are equal.

For example, "tars"and "rats"are similar (swapping at positions 0 and 2), and "rats" and "arts" are similar, but "star" is not similar to "tars", "rats", or "arts".

Together, these form two connected groups by similarity: {"tars", "rats", "arts"} and {"star"}. Notice that "tars" and "arts" are in the same group even though they are not similar. Formally, each group is such that a word is in the group if and only if it is similar to at least one other word in the group.

We are given a list strs of strings where every string in strs is an anagram of every other string in strs. How many groups are there?

Example 1:
```
Input: strs = ["tars","rats","arts","star"]
Output: 2
```

Example 2:
```
Input: strs = ["omv","ovm"]
Output: 1
```

Constraints:
* 1 <= strs.length <= 300
* 1 <= strs[i].length <= 300
* strs[i] consists of lowercase letters only.
* All words in strs have the same length and are anagrams of each other.

<br />

## Sample C++ Code Breadth-First Search 


```c
class Solution {
public:
    bool isSimilar(string a, string b){
        if (a == b) return true;
        int diff = 0;
        for (int i = 0; i < a.size(); i++) {
            if (a[i] != b[i]) 
                diff++;
        }
        return (diff == 0 || diff == 2) ? true : false;
    }
    
    int numSimilarGroups(vector<string>& strs) {
        int n = strs.size();
        if (n == 1) return 1;

        int groups = 0;
        vector<bool> visited(n, false);

        for (int i = 0; i < n; i++) {
          if (visited[i]) continue;
          groups++;
          visited[i] = true;
          queue<int> q;
          q.push(i);
          while (!q.empty()) {
              string comp = strs[q.front()];
              q.pop();
              for (int j = 0; j < n; j++) {
                  if (visited[j] || i == j) continue;
                  if (isSimilar(comp, strs[j])) {
                      q.push(j);
                      visited[j] = true;
                  }
              }
          }
        }
        return groups;        
    }
};
```


