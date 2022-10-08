---
layout: post
title: "Find The Town Judge Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, Graph ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 997. In a town, there are n people labeled from 1 to n. There is a rumor that one of these people is secretly the town judge.

---

<br />

## Description

LeetCode Problem 997.

In a town, there are n people labeled from 1 to n. There is a rumor that one of these people is secretly the town judge.

If the town judge exists, then:
* The town judge trusts nobody.
* Everybody (except for the town judge) trusts the town judge.
* There is exactly one person that satisfies properties 1 and 2.

You are given an array trust where trust[i] = [a_i, b_i] representing that the person labeled a_i trusts the person labeled b_i.

Return the label of the town judge if the town judge exists and can be identified, or return -1 otherwise.

Example 1:
```
Input: n = 2, trust = [[1,2]]
Output: 2
```

Example 2:
```
Input: n = 3, trust = [[1,3],[2,3]]
Output: 3
```

Example 3:
```
Input: n = 3, trust = [[1,3],[2,3],[3,1]]
Output: -1
```

Example 4:
```
Input: n = 3, trust = [[1,2],[2,3]]
Output: -1
```

Example 5:
```
Input: n = 4, trust = [[1,3],[1,4],[2,3],[2,4],[4,3]]
Output: 3
```

Constraints:
* 1 <= n <= 1000
* 0 <= trust.length <= 10^4
* trust[i].length == 2
* All the pairs of trust are unique.
* a_i != b_i
* 1 <= a_i, b_i <= n

<br />

## Sample C++ Code


```c
class Solution {
public:
    int findJudge(int N, vector<vector<int>>& trust) {
        unordered_map<int, int> m;
        for (int i = 1; i <= N; i ++) 
            m[i] = 0;
        for (int i = 0; i < trust.size(); i ++) {
            m[trust[i][0]] --;
            m[trust[i][1]] ++;
        }
        for (int i = 1; i <= N; i ++) {
            if (m[i] == N-1)
                return i;
        }
        return -1;
    }
};
```


