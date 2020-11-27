---
layout: post
title:  "Polymorphism in C++"
categories: [ C++ Concepts ]
tags: [ C++, Polymorphism, Overload, Override, Virtual Function, Pure Virtual Function ]
similar: [ C++ OOP ]
featured: false
hidden: false
excerpt: Polymorphism means having more than one function with the same name but with different functionalities. 
---

<br />

## Polymorphism

`Polymorphism` means many forms. Polymorphism means having more than one function with the same name but with different functionalities. 

C++ polymorphism means that a call to a member function will cause a different function to be executed depending on the type of object that invokes the function.

Polymorphism is of two types: 1. `Static polymorphism` is also known as early binding. 2. `Dynamic polymorphism` is also known as late binding.

<br />

## Static Polymorphism

There are two types of static polymorphism: `function overloading` and `operator overloading`.

Function overloading means multiple functions with the same name have different functionalities. Functions can be overloaded by change in number of arguments or/and change in type of arguments.
Similarly, operators can be overload in C++.

```c
#include <iostream>

using namespace std;

class Complex {
private:
	int real, imag;
public:
	// Function overloading
	Complex() {
		real = 0;
		imag = 0;
	}
	Complex(int r) {
		real = r;
		imag = 0;
	}
	Complex(int r, int i) {
		real = r;
		imag = i;
	}

	// Operator overloading
	Complex operator + (Complex const &obj) {
		Complex res(real+obj.real, imag+obj.imag);
		return res;
	}

	void print() {
		cout << real << " + i" << imag << endl;
	}
};

int main() {
	Complex c1(10), c2(2, 4);
	Complex c3 = c1 + c2;
	c3.print();
}
```



<br />

## Dynamic Polymorphism

Dynamic polymorphism occurs when there is a hierarchy of classes and they are related by inheritance. This type of polymorphism is achieved by `function overriding`.

Consider the following example where a base class is derived by two other classes.

```c
#include <iostream>
using namespace std;

class Base {
public:
	int print() {
		cout << "Print from Base Class." << endl;
	}
};

class Derived1: public Base {
public:
	int print() {
		cout << "Print from Derived1 Class." << endl;
	}
};

class Derived2: public Base {
public:
	int print() {
		cout << "Print from Derived2 Class." << endl;
	}
};

int main() {
	Base *b;

	Derived1 d1;
	Derived2 d2;

	b = &d1;
	b->print();

	b = &d2;
	b->print();

	return 0;
}
```

The output of this program is:
```
Print from Base Class.         
Print from Base Class.
```

This is because the call to the function print() is set during the compilation of the program (`early binding`). This is called `static resolution` of the function call - the function call is fixed before the program is executed.


To make polymorphism work, we need to use the `virtual function`. If we modify the Base class as below (add the keyword **virtual** in the base class' print() function):
```c
class Base {
public:
	virtual int print() {
		cout << "Print from Base Class." << endl;
	}
};
```

The output of the program is:
```
Print from Derived1 Class.
Print from Derived2 Class.
```

This time, the compiler looks at the contents of the pointer instead of its type. Thus, the print() functions from the derived classes are called. 

The function to be called is based on the kind of object for which it is called. This is called `late binding`.

It is possible that we would like to include a virtual function in the base class so that it may be redefined in a derived class to suit the objects of that class, but there is no meaningful definition we could give for the function in the base class. We can use the `pure virtual function` here.

```c
class Base {
public:
	virtual int print() = 0;
};
```

The difference between virtual function and pure virtual function is whether there is content in the function body. Note that a class containing pure virtual function cannot be instantiated.










