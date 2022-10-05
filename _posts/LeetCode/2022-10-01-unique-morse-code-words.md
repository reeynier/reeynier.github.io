---
layout: post
title: "Unique Morse Code Words Problem"
categories: [ Algorithm, Data Structure ]
tags: [ Array, Hash Table, String ]
similar: [ Hash Table ]
featured: false
hidden: false
excerpt: LeetCode 804. International Morse Code defines a standard encoding where each letter is mapped to a series of dots and dashes, as follows

---

<br />

## Description

LeetCode Problem 804.

International Morse Code defines a standard encoding where each letter is mapped to a series of dots and dashes, as follows:
* 'a' maps to ".-",
* 'b' maps to "-...",
* 'c' maps to "-.-.", and so on.

For convenience, the full table for the 26 letters of the English alphabet is given below:
```
[".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
```

Given an array of strings words where each word can be written as a concatenation of the Morse code of each letter.
* For example, "cab" can be written as "-.-..--...", which is the concatenation of "-.-.", ".-", and "-...". We will call such a concatenation the transformation of a word.

Return the number of different transformations among all words we have.

Example 1:
```
Input: words = ["gin","zen","gig","msg"]
Output: 2
Explanation: The transformation of each word is:
"gin" -> "--...-."
"zen" -> "--...-."
"gig" -> "--...--."
"msg" -> "--...--."
There are 2 different transformations: "--...-." and "--...--.".
```

Example 2:
```
Input: words = ["a"]
Output: 1
```

Constraints:
* 1 <= words.length <= 100
* 1 <= words[i].length <= 12
* words[i] consists of lowercase English letters.

<br />

## Sample C++ Code


```c
class Solution {
public:
    int uniqueMorseRepresentations(vector<string>& words) {
        vector<string> morse_code = { ".-", "-...", "-.-.", "-..", ".",
        	"..-.", "--.", "....", "..", ".---", "-.-", ".-..", "--",
        	"-.", "---", ".--.", "--.-", ".-.", "...", "-", "..-",
        	"...-", ".--", "-..-", "-.--", "--.." };
        unordered_set<string> gen_codes;

        for (auto word : words) {
            string code = "";
            for (auto ch : word)
                code += morse_code[ch - 'a'];
            gen_codes.insert(code);
        }

        return gen_codes.size();
    }
};
```


