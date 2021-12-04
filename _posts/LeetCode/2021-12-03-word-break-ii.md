---
layout: post
title: "Word Break II Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Dynamic Programming, Backtracking, Trie, Memoization]
similar: [ Trie]
featured: false
hidden: false
excerpt: LeetCode 140. Given a string s and a dictionary of strings wordDict, add spaces in s to construct a sentence where each word is a valid dictionary word. Return all such possible sentences in any order.
---

<br />

## Description

LeetCode Problem 140.

Given a string s and a dictionary of strings wordDict, add spaces in s to construct a sentence where each word is a valid dictionary word. Return all such possible sentences in any order.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

Example 1:
```
Input: s = "catsanddog", wordDict = ["cat","cats","and","sand","dog"]
Output: ["cats and dog","cat sand dog"]
```

Example 2:
```
Input: s = "pineapplepenapple", wordDict = ["apple","pen","applepen","pine","pineapple"]
Output: ["pine apple pen apple","pineapple pen apple","pine applepen apple"]
Explanation: Note that you are allowed to reuse a dictionary word.
```

Example 3:
```
Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: []
```

Constraints:
* 1 <= s.length <= 20
* 1 <= wordDict.length <= 1000
* 1 <= wordDict[i].length <= 10
* s and wordDict[i] consist of only lowercase English letters.
* All the strings of wordDict are unique.

<br />

## Sample C++ Code


```c
class Solution {
public:
    struct TrieNode {
        TrieNode* arr[26];
        bool is_end;
        TrieNode() {
            for (int i = 0; i < 26; i ++) arr[i] = nullptr;
            is_end = false;
        }
    };
    
    void insert(TrieNode* root, string s) {
        TrieNode* curr = root;
        for (int i = 0; i < s.size(); i ++) {
            if (curr->arr[s[i]-'a'] == nullptr)
                curr->arr[s[i]-'a'] = new TrieNode();
            curr = curr->arr[s[i]-'a'];
        }
        curr->is_end = true;
        return;
    }
    
    vector<string> ans;
    
    void dfs(string& currS, string& s, int idx, TrieNode* root) {
        if (idx == s.size()) {
            ans.push_back(currS.substr(0, currS.size()-1));
        }    
        if (idx >= s.size())
            return;
        
        TrieNode* curr = root;
        string tempS;
        for (int i = idx; i < s.size(); i ++) {
            tempS += s[i];
            if (curr->arr[s[i]-'a'] == nullptr)
                return;
            curr = curr->arr[s[i]-'a'];
            if (curr->is_end == true) {
                currS = currS + tempS + ' ';
                dfs(currS, s, i+1, root);
                currS = currS.substr(0, currS.size()-tempS.size()-1);
            }
        }
    }
    
    vector<string> wordBreak(string s, vector<string>& wordDict) {
        TrieNode* root = new TrieNode();
        for (int i = 0; i < wordDict.size(); i ++) {
            insert(root, wordDict[i]);
        }
        
        string currS;
        dfs(currS, s, 0, root);
        return ans;
    }
};
```


