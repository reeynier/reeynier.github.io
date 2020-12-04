---
layout: post
title:  "Explicit Type Conversions in C++"
categories: [ C++ Concepts ]
tags: [ C++, Type Conversion, Cast ]
similar: [ C++ Basic ]
featured: false
hidden: false
excerpt: An `explicit conversion` is also called as a `cast`. There are four cast opeartors, *static_cast*, *dynamic_cast*, *const_cast*, and *reinterpret_cast*.
---

<br />

## Explicit Type Conversions

An `explicit conversion` is also called as a `cast`. There are four cast opeartors: *static_cast*, *dynamic_cast*, *const_cast*, and *reinterpret_cast*.


#### When Casts Might Be Useful

1. One reason to perform an explicit cast is to override the usual standard conversions.

	```
	// ival is converted to double in order to be multiplied by dval
	// The double result is then truncated to int in order to assign it to ival
	double dval;
	int ival;
	ival = ival * dval;

	// Or we can eliminate the unnecessary conversion of ival to double
	// by explicitly casting dval to int
	ival *= static_cast<int>(dval);
	```

2. Another reason is to select a specific conversion when more than one conversion is possible. This situation is discussed in overloading.

#### Named Casts

1. dynamic_cast

	A `dynamic_cast` supports the run-time identification of objects addressed either by a pointer or reference.

	```
	if (Derived *derivedPtr = dynamic_cast<Derived*>(basePtr)) {
		// use the Derived Object to which derivedPtr points
	} else {  // BasePtr points at a Base Object
		// use the Base Object to which basePtr points
	}
	```

	In the above example, assume Base is a class with at least one virtual function and that class Derived is derived from Base. We have a pointer to Base named basePtr. At run time, if basePtr actually points to a Derived object, the cast will be successfull, and derivedPtr will be initialized to point to the Derived object to which basePtr points. Otherwise, the result of the cast is 0, meaning the derivedPtr is set to 0, and the if condition fails.

2. const_cast

	A `const_cast` converts a const value to a normal value (casts away the const-ness). For example, the follwing string_copy function takes a char\* type parameter. So when we pass the pc_str to it, we need to convert it to a non-const type parameter.

	```
	const char *pc_str;
	char *pc = string_copy(const_cast<char*>(pc_str));
	```

3. static_cast

	A `static_cast` is useful to perform a conversion that the compiler will not generate automatically. For example, we can use a static_cast to retrieve a pointer value that was stored in a void\* pointer.

	```
	// address of any data object can be stored in a void*
	void* p = &d; 
	// converts void* back to the original pointer type
	// we are guaranteed that the pointer value is preserved
	double *dp = static_cast<double*>(p);
	```

4. reinterpret_cast

	A `reinterpret_cast` generally performs a low-level reinterpretation of the bit pattern of its operands.

	```
	int *ip;
	char *pc = reinterpret_cast<char*>(ip);
	```

	The actual object addressed by pc is **always** an int, not a character array. Any use of pc that assumes its an ordinary character pointer is likely to **fail at run time**.

#### Old Style Casts


Prior to the introduction of named cast operators, an explicit cast was performed by enclosing a type in parentheses:

```
char *pc = (char*) ip;
```

The effect of this cast is the same as using the reinterpret_cast notation. Depending on the types involved, an `old-style cast` has the same behavior as a const_cast, a static_cast, or a reinterpret_cast.

```
int ival; double dval;
ival += int (dval); // static_cast: converts double to int 

const char* pc_str;
string_copy((char*)pc_str); // const_cast: casts away const

int *ip;
char *pc = (char*)ip; // reinterpret_cast: treats int* as char*
```

Standard C++ introduced the named cast operators to make casts more visible and to give the programmer a more finely tuned tool to use when casts are necessary.









