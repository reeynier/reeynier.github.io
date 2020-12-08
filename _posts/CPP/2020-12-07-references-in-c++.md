---
layout: post
title:  "References in C++"
categories: [ C++ Concepts ]
tags: [ C++, Reference, Lvalue Reference, Rvalue Reference ]
similar: [ C++ Reference ]
featured: false
hidden: false
excerpt: A reference is an alias of another object. It stores the address of an object that is located elsewhere in memory.
---

<br />

This post and the examples are from the [Microsoft C++ Documentation](https://docs.microsoft.com/en-us/cpp/cpp/references-cpp?view=msvc-160){:target="_blank"}. 



A reference is an alias of another object. It stores the address of an object that is located elsewhere in memory. Unlike a pointer, a reference cannot be set to NULL when initializing, and cannot be reassigned to refer to a different object after initialization. 

There are two kinds of references: `lvalue references`  which refer to a named variable, and `rvalue references` which refer to a temporary object. The & operator signifies an lvalue reference and the operator signifies either an rvalue reference, or a universal reference (either rvalue or lvalue depending on the context).

Below is an example of using references.

```c
#include <stdio.h>
struct S {
    short i;
};

int main() {
    S  s;   // Declare the object.
    S& SRef = s;   // Declare the reference.
    s.i = 3;

    printf_s("%d\n", s.i);
    printf_s("%d\n", SRef.i);

    SRef.i = 4;
    printf_s("%d\n", s.i);
    printf_s("%d\n", SRef.i);
}
```


The output of the above coe is:
```
3
3
4
4
```

When changing the i value of either s or SRef, the other one changes too. This is because both SRef and s are pointing to the same object.

































































