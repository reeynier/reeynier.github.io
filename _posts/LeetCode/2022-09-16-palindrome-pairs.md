---
layout: post
title: "Palindrome Pairs Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, String, Trie ]
similar: [ Trie ]
featured: false
hidden: false
excerpt: LeetCode 336. Given a list of unique words, return all the pairs of the distinct indices (i, j) in the given list, so that the concatenation of the two wordswords[i] + words[j] is a palindrome.

---

<br />

## Description

LeetCode Problem 336.

Given a list of unique words, return all the pairs of the<i>distinct</i> indices (i, j) in the given list, so that the concatenation of the two wordswords[i] + words[j] is a palindrome.

Example 1:
```
Input: words = ["abcd","dcba","lls","s","sssll"]
Output: [[0,1],[1,0],[3,2],[2,4]]
Explanation: The palindromes are ["dcbaabcd","abcddcba","slls","llssssll"]
```

Example 2:
```
Input: words = ["bat","tab","cat"]
Output: [[0,1],[1,0]]
Explanation: The palindromes are ["battab","tabbat"]
```

Example 3:
```
Input: words = ["a",""]
Output: [[0,1],[1,0]]
```

Constraints:
* 1 <= words.length <= 5000
* 0 <= words[i].length <= 300
* words[i] consists of lower-case English letters.

<br />

## Sample C++ Code


```c
struct TrieNode {
    TrieNode *next[26] = {};
    int index = -1;
    vector<int> palindromeIndexes;
};

class Solution {
    TrieNode root; // Suffix trie
    void add(string &s, int i) {
        auto node = &root;
        for (int j = s.size() - 1; j >= 0; --j) {
            if (isPalindrome(s, 0, j)) 
            	// A[i]'s prefix forms a palindrome
            	node->palindromeIndexes.push_back(i); 
            int c = s[j] - 'a';
            if (!node->next[c]) 
            	node->next[c] = new TrieNode();
            node = node->next[c];
        }
        node->index = i;
        // A[i]'s prefix is empty string here, which is a palindrome.
        node->palindromeIndexes.push_back(i); 
    }
    
    bool isPalindrome(string &s, int i, int j) {
        while (i < j && s[i] == s[j]) 
        	++i, --j;
        return i >= j;
    }
    
public:
    vector<vector<int>> palindromePairs(vector<string>& A) {
        int N = A.size();
        for (int i = 0; i < N; ++i) 
        	add(A[i], i);
        vector<vector<int>> ans;
        for (int i = 0; i < N; ++i) {
            auto s = A[i];
            auto node = &root;
            for (int j = 0; j < s.size() && node; ++j) {
                if (node->index != -1 && node->index != i && isPalindrome(s, j, s.size() - 1)) ans.push_back({ i, node->index }); 
                // A[i]'s prefix matches this word and A[i]'s suffix forms a palindrome
                node = node->next[s[j] - 'a'];
            }
            if (!node) continue;
            for (int j : node->palindromeIndexes) { 
                // A[i] is exhausted in the matching above. 
                // If a word whose prefix is palindrome after matching its suffix with A[i], 
                // then this is also a valid pair
                if (i != j) ans.push_back({ i, j });
            }
        }
        return ans;
    }
};
```


