---
layout: post
title: "Goat Latin Problem"
categories: [ Algorithm, Data Structure ]
tags: [ String ]
similar: [ String ]
featured: false
hidden: false
excerpt: LeetCode 824. You are given a string sentence that consist of words separated by spaces. Each word consists of lowercase and uppercase letters only.

---

<br />

## Description

LeetCode Problem 824.

You are given a string sentence that consist of words separated by spaces. Each word consists of lowercase and uppercase letters only.

We would like to convert the sentence to "Goat Latin" (a made-up language similar to Pig Latin.) The rules of Goat Latin are as follows:
* If a word begins with a vowel ('a', 'e', 'i', 'o', or 'u'), append "ma" to the end of the word.
* For example, the word "apple" becomes "applema".
* If a word begins with a consonant (i.e., not a vowel), remove the first letter and append it to the end, then add "ma".
* For example, the word "goat" becomes "oatgma".
* Add one letter 'a' to the end of each word per its word index in the sentence, starting with 1.
* For example, the first word gets "a" added to the end, the second word gets "aa" added to the end, and so on.

Return the final sentence representing the conversion from sentence to Goat Latin.

Example 1:
```
Input: sentence = "I speak Goat Latin"
Output: "Imaa peaksmaaa oatGmaaaa atinLmaaaaa"
```

Example 2:
```
Input: sentence = "The quick brown fox jumped over the lazy dog"
Output: "heTmaa uickqmaaa rownbmaaaa oxfmaaaaa umpedjmaaaaaa overmaaaaaaa hetmaaaaaaaa azylmaaaaaaaaa ogdmaaaaaaaaaa"
```

Constraints:
* 1 <= sentence.length <= 150
* sentence consists of English letters and spaces.
* sentence has no leading or trailing spaces.
* All the words in sentence are separated by a single space.

<br />

## Sample C++ Code


```c
class Solution {
public:
    string toGoatLatin(string S) {
        unordered_set<char> vowel({'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'});
        istringstream iss(S);
        string res, w;
        int i = 0, j;
        while (iss >> w) {
            res += ' ' + (vowel.count(w[0]) == 1 ? w : w.substr(1) + w[0]) + "ma";
            for (j = 0, ++i; j < i; ++j) 
                res += "a";
        }
        return res.substr(1);
    }
};
```


