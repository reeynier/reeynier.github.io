---
layout: post
title:  "Interfaces in C++"
categories: [ C++ Concepts ]
tags: [ C++, Interface, Abstract Class, Pure Virtual Function, Concrete Class ]
similar: [ C++ OOP ]
featured: false
hidden: false
---

<br />

## Interfaces and Abstract Classes

An `interface` describes the behavior or capabilities of a C++ class without committing to a particular implementation of that class.

The C++ interfaces are implemented using `abstract classes` and these abstract classes should not be confused with data abstraction which is a concept of keeping implementation details separate from associated data.

A class is made abstract by declaring at least one of its functions as `pure virtual function`. A pure virtual function is specified by placing "= 0" in its declaration.


```c
class Base {
public:
	virtual int print() {
		cout << "Print from Base Class." << endl;
	}
};
```


The purpose of an `abstract class` is to provide an appropriate base class from which other classes can inherit. Abstract classes cannot be used to instantiate objects and serves only as an `interface`. Attempting to instantiate an object of an abstract class causes a compilation error.


Thus, if a subclass of an abstract class needs to be instantiated, it has to implement each of the virtual functions. Failure to override a pure virtual function in a derived class, then attempting to instantiate objects of that class, is a compilation error.

Classes that can be used to instantiate objects are called `concrete classes`.






