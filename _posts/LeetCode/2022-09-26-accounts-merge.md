---
layout: post
title: "Accounts Merge Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, String, Depth-First Search, Breadth-First Search, Union Find ]
similar: [ Union Find ]
featured: false
hidden: false
excerpt: LeetCode 721. Given a list of accounts where each element accounts[i] is a list of strings, where the first element accounts[i][0] is a name, and the rest of the elements are emails representing emails of the account.

---

<br />

## Description

LeetCode Problem 721.

Given a list of accounts where each element accounts[i] is a list of strings, where the first element accounts[i][0] is a name, and the rest of the elements are emails representing emails of the account.

Now, we would like to merge these accounts. Two accounts definitely belong to the same person if there is some common email to both accounts. Note that even if two accounts have the same name, they may belong to different people as people could have the same name. A person can have any number of accounts initially, but all of their accounts definitely have the same name.

After merging the accounts, return the accounts in the following format: the first element of each account is the name, and the rest of the elements are emails in sorted order. The accounts themselves can be returned in any order.

Example 1:
```
Input: accounts = [["John","johnsmith@mail.com","john_newyork@mail.com"],["John","johnsmith@mail.com","john00@mail.com"],["Mary","mary@mail.com"],["John","johnnybravo@mail.com"]]
Output: [["John","john00@mail.com","john_newyork@mail.com","johnsmith@mail.com"],["Mary","mary@mail.com"],["John","johnnybravo@mail.com"]]
Explanation:
The first and second John's are the same person as they have the common email "johnsmith@mail.com".
The third John and Mary are different people as none of their email addresses are used by other accounts.
We could return these lists in any order, for example the answer [['Mary', 'mary@mail.com'], ['John', 'johnnybravo@mail.com'], 
['John', 'john00@mail.com', 'john_newyork@mail.com', 'johnsmith@mail.com']] would still be accepted.
```

Example 2:
```
Input: accounts = [["Gabe","Gabe0@m.co","Gabe3@m.co","Gabe1@m.co"],["Kevin","Kevin3@m.co","Kevin5@m.co","Kevin0@m.co"],["Ethan","Ethan5@m.co","Ethan4@m.co","Ethan0@m.co"],["Hanzo","Hanzo3@m.co","Hanzo1@m.co","Hanzo0@m.co"],["Fern","Fern5@m.co","Fern1@m.co","Fern0@m.co"]]
Output: [["Ethan","Ethan0@m.co","Ethan4@m.co","Ethan5@m.co"],["Gabe","Gabe0@m.co","Gabe1@m.co","Gabe3@m.co"],["Hanzo","Hanzo0@m.co","Hanzo1@m.co","Hanzo3@m.co"],["Kevin","Kevin0@m.co","Kevin3@m.co","Kevin5@m.co"],["Fern","Fern0@m.co","Fern1@m.co","Fern5@m.co"]]
```

Constraints:
* 1 <= accounts.length <= 1000
* 2 <= accounts[i].length <= 10
* 1 <= accounts[i][j] <= 30
* accounts[i][0] consists of English letters.
* accounts[i][j] (for j > 0) is a valid email.

<br />

## Sample C++ Code using Union Find 


```c
class Solution {
public:
    
    int _find(int p, vector<int>& nums) {
        while (p != nums[p]) {
            p = nums[p];
        }
        return p;
    }
    
    void _union(int i, int j, vector<int>& nums) {
        int r1 = _find(i, nums);
        int r2 = _find(j, nums);
        
        nums[r1] = r2;
        
    }
    
    vector<vector<string>> accountsMerge(vector<vector<string>>& accounts) {
        int n = accounts.size();
        
        unordered_map<string, int> ht;
        vector<int> parent;
        for (int i = 0; i < n; i ++) parent.push_back(i);
        
        for (int i = 0; i < n; i ++) {
            for (int j = 1; j < accounts[i].size(); j ++) {
                if (ht.find(accounts[i][j]) == ht.end()) {
                    ht[accounts[i][j]] = i;
                } else {
                    _union(ht[accounts[i][j]], i, parent);
                }
            }
        }
        
        unordered_map<int, set<string>> htset;
        for (int i = 0; i < n; i ++) {
            int root = _find(i, parent);
            set<string> temp = set<string>(accounts[i].begin(), accounts[i].end());
            if (htset.find(root) == htset.end())
                htset[root] = temp;
            else
                htset[root].insert(temp.begin(), temp.end());
        }
        
        vector<vector<string>> ans;
        for (auto x : htset) {
            ans.push_back(vector<string>(x.second.begin(), x.second.end()));
        }
        return ans;
        
    }
};
```


