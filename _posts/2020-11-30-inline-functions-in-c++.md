---
layout: post
title:  "Inline Functions in C++"
categories: [ C++ Concepts ]
tags: [ C++, Inline Functions ]
similar: [ C++ OOP ]
featured: false
hidden: false
excerpt: An `interface` describes the behavior or capabilities of a C++ class without committing to a particular implementation of that class.
---

<br />

## Inline Functions

Consider a function that returns a reference to the shorter of its two string parameters:
```
// finder shorter of two strings
const string &shorterString(const string &s1, const string &s2) {
	return s1.size() < s2.size() ? s1 : s2;
}
```

The benefits of using a function call include:

* It is easier to read and understand.
* It is easier to make changes than to find and change every occurrence of the equivalent expression.
* It is easier to reuse this piece of code.
* It is easier to test the code.

However, there is one potential drawback to making such a small piece of code a function. Calling a function is slower than evaluating the equivalent expression. This is because a function call does a lot of work: registers are saved before the call and restored after the return; stack space are allocated; the arguments are copied; and the program branches to a new location. This can result in a substantial performance penalty.

#### `Inline` Functions Avoid Function Call Overhead

A function specified as `inline` is expanded everywhere it is invoked. If we make the *shorterString* an inline function, then this call:
```
cout << shorterString(s1, s2) << endl;
```

will be expanded during compilation into:
```
cout << (s1.size() < s2.size() ? s1 : s2) << endl;
```

The run-time overhead of making *shorterString* a function is thus removed.

To define the *shorterString* function as an inline function, we just put the keyword *inline* before the function's return type.
```
// inline version: find shorter of two strings
inline const string &shorterString(const string &s1, const string &s2) {
	return s1.size() < s2.size() ? s1 : s2;
}
```

Note that the inline specification is only a **request** to the compiler. The compiler may choose to ignore the request if it is a recursive function or a super long function.


Unlike other function definitions, inlines should be defined in header files. Whenever an inline function is added to or changed in a header file, every source file that uses that header must be recompiled.































