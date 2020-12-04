---
layout: post
title:  "Implicit Type Conversions in C++"
categories: [ C++ Concepts ]
tags: [ C++, Type Conversion ]
similar: [ C++ Basic ]
featured: false
hidden: false
excerpt: C++ transforms the operands to a common type before performing the arithmetic. These conversions are carried out automatically by the compiler, and are referred to as `implicit type conversions`.
---

<br />

## Implicit Type Conversions

Consider the following example:
```
int ival = 0;
ival = 3.541 + 3; // typically compiles with a warning
```
In this example, ival is assigned with value 6. The operands to the addition operator are values of two different types: 3.541 is a literal of type *double*, and 3 is a literal of type *int*. Instead of trying to add values of two different types, C++ transforms the operands to a common type before performing the arithmetic. These conversions are carried out automatically by the compiler, and are referred to as `implicit type conversions`.


The built-in conversions among the arithmetic types are defined to preserve precision, if possible. Thus, in this example, the interger 3 is converted to double. Then floating point addition is performed and the result is 6.541.

The next step is to assign the double value to ival, which is an integer. In the case of assignment, the type of the left-hand operand dominates, because it is not possible to change the type of the object on the left-hand side. So the double value 6.541 is converted to int, which becomes 6. Because the conversion of a double to int may result in a loss of precision, most compilers issue a warning.

 


#### When Implicit Type Conversions Occur

Implicit type conversions occur in the following situations:

* In expressions with operands of mixed types:

```
int ival;
double dval;
ival >= dval  // ival is converted to double
```

* An expression used as a condition is converted to bool:

```
int ival;
if (ival)   // ival is converted to bool
while (ival)  // ival is converted to bool
```

* An expression used to initialize or assign to a variable is converted to the type of the variable:

```
int ival = 3.14  // 3.14 is converted to int
int *ip;
ip = 0;  // the int 0 is converted to a null pointer of type int*
```


#### The Arithmetic Conversions

C++ defines a set of conversions among the built-in types. The most common are the `arithmetic conversions`, which ensure that the two operands of a binary operator are converted to a common type before the operator is evaluated. Here are some conversion rules:

1. Preserve the precision of the values involved in a multi-type expression.

    Please refer to the first exmaple in this post.

2. Conversions are in a hierarchy. Operands are converted to the widest type in the expression.

    Each of the integral types that are smaller than *int char*, *signed char*, *unsigned char*, *short*, and *unsigned short* is promoted to *int* if all possible values of that type fit in an *int*. Otherwise, the value is promoted to *unsigned int*.

3. When an unsigned value is involved in an expression, preserve the value of the operands.

    Among operands of type *long* and *unsigned int*, the *unsigned int* operand is converted to *long* if type *long* on the machine is large enough to represent all the values of the *unsigned int*. Otherwise, both operands are converted to *unsigned long*.

4. When both signed and unsigned int are involved, the signed value is converted to unsigned.
  

#### The Pointer Conversions

1. In most cases when we use an array, the array is automatically converted to a pointer to the first element.

```
int ia[10];   // array of 10 ints
int* ip = ia; // convert ia to pointer to first element
```

2. A pointer to any data type can be converted to a void\*. And a void\* can be converted to a pointer to any data type.

3. The constant value 0 can be converted to any pointer type.


#### The Bool Conversions

1. Arithmetic and pointer values can be converted to bool. If the pointer or arithmetic value is zero, then the bool is False; any other value converts to True.

2. Bool objects can be converted to int -- true becomes 1 and false becomes 0.


#### The Enumeration Types Conversions

Objects of an enumeration type or an enumerator can be automatically converted to an integral type. 

```
// point2d is 2, point2w is 3, point3d is 3, point3w is 4 
enum Points { point2d = 2, point2w, point3d = 3, point3w };
```

#### Conversion to Const

A non-const object can be converted to a const object, which happens when we use a non-const object to initialize a reference to const object. We can also convert the address of a non-const object to a pointer to the related const type.

```
int i;
const int ci = 0;
const int &j = i;    // convert non-const to reference to const int
const int *p = &i;  // convert address of non-const to address of a const
```














