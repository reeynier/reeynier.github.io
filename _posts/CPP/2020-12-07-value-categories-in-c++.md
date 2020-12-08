---
layout: post
title:  "Value Categories in C++"
categories: [ C++ Concepts ]
tags: [ C++, Reference, Lvalue Reference, Rvalue Reference ]
similar: [ C++ Basic ]
featured: false
hidden: false
excerpt: Every C++ expression has a type and belongs to a value category. 
---

<br />

This post and the examples are from the [Microsoft C++ Documentation](https://docs.microsoft.com/en-us/cpp/cpp/lvalues-and-rvalues-visual-cpp?view=msvc-160){:target="_blank"}. 

#### Value Categories

Every C++ expression has a type and belongs to a `value category`. The value categories are the basis for rules that compilers must follow when creating, copying, and moving temporary objects during expression evaluation. 

The C++ 17 standard defines expression value categories as follows:

* A `glvalue` is an expression whose evaluation determines the **identity** of an object, bit-field, or function.

* A `prvalue` is an expression whose evaluation **initializes** an object or a bit-field, or computes the value of the operand of an operator, as specified by the context in which it appears. It has no address that is accessible by the program. Examples include literals, function calls that return a non-reference type, and temporary objects that are created during expression evaluation but accessible only by the compiler.

* A `xvalue` is a glvalue that denotes an object or bit-field whose resources can be reused. It has an address that no longer accessible by the program, but can be used to initialize an rvalue reference. Examples include function calls that return an rvalue reference, and the array subscript, member, and pointer to member expressions where the array or object is an rvalue reference.

* An `lvalue` is a glvalue that is not an xvalue. It has an address that the program can access. An example is the variable names.

* An `rvalue` is a prvalue or an xvalue. 




The following figure illustrates the relationships between the categories.

```
        expression
          /   \
    glvalue   rvalue
     /   \     /   \
lvalue    xvalue    prvalue
```



#### An Example

The following example demonstrates several correct and incorrect usages of lvalues and rvalues:

```c
int main()
{
    int i, j, *p;

    // Correct usage: the variable i is an lvalue and the literal 7 is a prvalue.
    i = 7;

    // Incorrect usage: The left operand must be an lvalue (C2106).`j * 4` is a prvalue.
    7 = i; // C2106
    j * 4 = 7; // C2106

    // Correct usage: the dereferenced pointer is an lvalue.
    *p = i;

    // Correct usage: the conditional operator returns an lvalue.
    ((i < 3) ? i : j) = 7;

    // Incorrect usage: the constant ci is a non-modifiable lvalue (C3892).
    const int ci = 7;
    ci = 9; // C3892
}
```






















































