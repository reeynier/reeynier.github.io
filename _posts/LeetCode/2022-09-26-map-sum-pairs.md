---
layout: post
title: "Map Sum Pairs Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Design, Trie ]
similar: [ Trie ]
featured: false
hidden: false
excerpt: LeetCode 677. Design a map that allows you to do the following

---

<br />

## Description

LeetCode Problem 677.

Design a map that allows you to do the following:
* Maps a string key to a given value.
* Returns the sum of the values that have a key with a prefix equal to a given string.
Implement the MapSum class:
* MapSum() Initializes the MapSum object.
* void insert(String key, int val) Inserts the key-val pair into the map. If the key already existed, the original key-value pair will be overridden to the new one.
* int sum(string prefix) Returns the sum of all the pairs' value whose key starts with the prefix.

Example 1:
```
Input
["MapSum", "insert", "sum", "insert", "sum"]
[[], ["apple", 3], ["ap"], ["app", 2], ["ap"]]
Output
[null, null, 3, null, 5]
Explanation
MapSum mapSum = new MapSum();
mapSum.insert("apple", 3);  
mapSum.sum("ap");           // return 3 (apple = 3)
mapSum.insert("app", 2);    
mapSum.sum("ap");           // return 5 (apple + app = 3 + 2 = 5)
```

Constraints:
* 1 <= key.length, prefix.length <= 50
* key and prefix consist of only lowercase English letters.
* 1 <= val <= 1000
* At most 50 calls will be made to insert and sum.

<br />

## Sample C++ Code using Trie 


```c
class MapSum {
public:
    struct TrieNode {
        map<char, TrieNode*> ht;
        int val;
        TrieNode() {
            val = 0;
        }
    };
    TrieNode* root;
    /** Initialize your data structure here. */
    MapSum() {
        root = new TrieNode();
    }
    
    void insert(string key, int val) {
        TrieNode* curr = root;
        for (int i = 0; i < key.size(); i ++) {
            if (curr->ht.find(key[i]) == curr->ht.end())
                curr->ht[key[i]] = new TrieNode();
            curr = curr->ht[key[i]];
        }
        curr->val = val;
    }
    
    int sum(string prefix) {
        int ans = 0;
        TrieNode* curr = root;
        for (int i = 0; i < prefix.size(); i ++) {
            if (curr->ht.find(prefix[i]) == curr->ht.end())
                return ans;
            curr = curr->ht[prefix[i]];
        }
        ans = addSum(curr);
        return ans;
    }
    
    int addSum(TrieNode* root) {
        int x = root->val;
        for (map<char, TrieNode*>::iterator mit = root->ht.begin(); 
            mit != root->ht.end(); mit ++) {
            x += addSum(mit->second);
        }
        return x;
    }
};

/**
 * Your MapSum object will be instantiated and called as such:
 * MapSum* obj = new MapSum();
 * obj->insert(key,val);
 * int param_2 = obj->sum(prefix);
 */
```


