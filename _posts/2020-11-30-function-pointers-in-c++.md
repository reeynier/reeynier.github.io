---
layout: post
title:  "Function Pointers in C++"
categories: [ C++ Concepts ]
tags: [ C++, Function Pointers, Pointers to Functions ]
similar: [ C++ Basic ]
featured: false
hidden: false
excerpt: An `interface` describes the behavior or capabilities of a C++ class without committing to a particular implementation of that class.
---

<br />

## Function Pointers

A `function pointer` is a pointer that denotes a function rather than an object. A function pointer points to a particular type. A function's type is determined by its return type and its parameter list. A function's name is not part of its type.

Below is an example of a function pointer declaration.
```
// pf points to function returning bool that takes two const string references
bool (*pf) (const string &, const string &);
```

This statement declars *pf* to be a function pointer that takes two *const string&* parameters and has a return type of *bool*.

Note that the parentheses around *\*pf* are necessary. Otherwise, it will be a declaration of a function *pf* that returns a *bool\**.
```
bool *pf (const string &, const string &);
```

#### Declaring, Initializing, Assigning Function Pointers
 
We can make function pointers easier to use by defining a synonym for the pointer type using a **typedef**. Below is an example definition.

```
typedef bool (*cmpFcn) (const string &, const string &);
```
This definition says that *cmpFcn* is the name of a type that is a pointer to function. When we need to use this function pointer type, we can do so by using *cmpFcn*, rather than having to write the full type definition each time.


When we use a function name without calling it, the name is automatically treated as a function pointer. A function pointer may be initialized or assigned only by a function or function pointer that has the same type or by a zero-valued constant expression. Here are the examples of how to initialize and assign function pointers. 
```
bool lengthCompare (const string &, const string &); 

cmpFcn pf1 = 0; // ok, the pointer does not point to any functions.
cmpFcn pf2 = lengthCompare; // ok, lengthCompare is treated as a function pointer, pointer type matches function's type
pf1 = lengthCompare;
pf2 = pf1;

// The following two usages are equivalent: using the function name is equivalent to applying the address-of operator to the function name.
cmpFcn pf1 = lengthCompare;
cmpFcn pf2 = &lengthCompare;
```

#### How To Use Function Pointers

Here are some examples of how to use function pointers. We can use the function pointers directly. There is no need to use the dereference operator to call the function.
```
cmpFcn pf = lengthCompare;
lengthCompare("hi", "bye"); // direct call
pf("hi", "bye"); // equivalent call: pf is implicitly dereferenced
(*pf)("hi", "bye"); // equivalent call: pf is explicitly dereferenced
```

#### Function Pointers As Parameters And Return Types

A function parameter can be a function pointer. We can write such a parameter in two ways.
```
// The third parameter is a function type and is automatically treated as a function pointer
void useBigger(const string &, const string &, bool(const string &, const string &));

// Equivalent declaration: explicitly define the parameter as a function pointer
void useBigger(const string &, const string &, bool (*)(const string &, const string &));
```

A function can return a function pointer.
```
// ff is a function taking an int an returning a function pointer
// the function pointed to returns an int and takes an int* and an int
int (*ff(int)) (int*, int);

// Or equivalently, use typedefs to make such declaration easier to read
// ff is a function taking one parameter of type int, and returns a function pointer type of pf
typedef int (*pf) (int*, int);
pf ff(int);
```







