---
layout: post
title: "Prefix And Suffix Search Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Hash Table, String, Design, Trie ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 745. Design a special dictionary with some words that searchs the words in it by a prefix and a suffix.

---

<br />

## Description

LeetCode Problem 745.

Design a special dictionary with some words that searchs the words in it by a prefix and a suffix.

Implement the WordFilter class:
* WordFilter(string[] words) Initializes the object with the words in the dictionary.
* f(string prefix, string suffix) Returns the index of the word in the dictionary, which has the prefix prefix and the suffix suffix. If there is more than one valid index, return the largest of them. If there is no such word in the dictionary, return -1.

Example 1:
```
Input
["WordFilter", "f"]
[[["apple"]], ["a", "e"]]
Output
[null, 0]
Explanation
WordFilter wordFilter = new WordFilter(["apple"]);
wordFilter.f("a", "e"); // return 0, because the word at index 0 has prefix = "a" and suffix = 'e".
```

Constraints:
* 1 <= words.length <= 15000
* 1 <= words[i].length <= 10
* 1 <= prefix.length, suffix.length <= 10
* words[i], prefix and suffix consist of lower-case English letters only.
* At most 15000 calls will be made to the function f.

<br />

## Sample C++ Code


```c
class WordFilter {
private:
    unordered_map<string, int> hashMap;

public:
    WordFilter(vector<string>& words) {
        int n = words.size();
        for (int i = 0; i < n; i++) {
            string word = words[i];
            int wordSize = word.size();
            for (int j = 1; j <= wordSize; j++) {
                string p = word.substr(0, j);
                for (int k = 0; k < wordSize; k++) {
                    string s = word.substr(k, wordSize);
                    hashMap[p + "|" + s] = i + 1;
                }
            }
        }
    }

    int f(string prefix, string suffix) {
        string s = prefix + "|" + suffix;
        return hashMap[s] - 1;
    }
};

/**
 * Your WordFilter object will be instantiated and called as such:
 * WordFilter* obj = new WordFilter(words);
 * int param_1 = obj->f(prefix,suffix);
 */
```


