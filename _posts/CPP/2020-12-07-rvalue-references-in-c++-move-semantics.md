---
layout: post
title:  "Rvalue References in C++: Move Semantics"
categories: [ C++ Concepts ]
tags: [ C++, Reference, Lvalue Reference, Rvalue Reference ]
similar: [ C++ Reference ]
featured: false
hidden: false
excerpt: The `rvalue references` enable us to distinguish an lvalue from an rvalue.
---

<br />

This post and the examples are from the [Microsoft C++ Documentation](https://docs.microsoft.com/en-us/cpp/cpp/rvalue-reference-declarator-amp-amp?view=msvc-160){:target="_blank"}. 



The `rvalue references` enable us to distinguish an lvalue from an rvalue (see [this post]({% post_url CPP/2020-12-07-value-categories-in-c++ %}) for more detail about value categories). In this post, we show how rvalue references support the implementation of move semantics.

#### Move Semantics

Rvalue references support the implementation of `move semantics`. Move semantics enable us to write code that transfers resources (such as dynamically allocated memory) from one object to another. To implement move semantics, we can provide a move constructor to a class, which is not provided by the compiler. Copy and assignment operations whose sources are rvalues then automatically take advantage of move semantics.

Consider the following example:
```c
#include <iostream>
#include <string>
using namespace std;

int main()
{
   string s = string("h") + "e" + "ll" + "o";
   cout << s << endl;
}
```

In this example, operator + cannot append one string to the other because it does not know whether the source strings are lvalues or rvalues. If the source strings are both lvalues, they might be referenced elsewhere in the program and therefore must not be modified. By using `rvalue references`, operator + can be modified to take rvalues, which cannot be referenced elsewhere in the program. Therefore, operator + can now append one string to another. This can significantly reduce the number of dynamic memory allocations that the string class must perform.


















































