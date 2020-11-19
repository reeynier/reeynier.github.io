---
layout: post
title:  "Smart Pointers in C++"
categories: [ C++ Concepts ]
tags: [ C++, Smart Pointers, RAII, Raw Pointers ]
similar: [ C++ ]
featured: false
hidden: false
---

<br />

This article is mainly from the Microsoft C++ Documentation. In modern C++ programming, the Standard Library includes `smart pointers`, which are used to help ensure that programs are free of memory and resource leaks and are exception-safe.

<br />

## Raw Pointers and Smart Pointers

`Smart pointers` are defined in the std namespace in the **memory** header file. They are crucial to the `RAII` (`Resource Acquisition Is Initialization`) programming idiom. The main principle of RAII is to give ownership of any *heap-allocated* resource to a *stack-allocated* object whose destructor contains the code to delete or free the resource and also any associated cleanup code.

In modern C++, `raw pointers` are only used in small code blocks where performance is critical and there is no chance of confusion about ownership. In most cases, when you initialize a raw pointer or resource handle to point to an actual resource, pass the pointer to a smart pointer immediately.

The following example compares a raw pointer declaration to a smart pointer declaration.

```c
void UseRawPointer() {
    // Using a raw pointer
    Song* pSong = new Song(L"Nothing on You", L"Bruno Mars");

    // Use pSong ...

    // Don't forget to delete!
    delete pSong;
}

void UseSmartPointer() {
    // Declare a smart pointer on stack and pass it the raw pointer.
    unique_ptr<Song> song2(new Song(L"Nothing on You", L"Bruno Mars"));

    // Use song2 ...
    wstring s = song2->duration_;
    // ...
} // song2 is deleted automatically here.
```

A `smart pointer` is a `class template` declared on the stack, and initialized by using a `raw pointer` that points to a heap-allocated object. After the smart pointer is intialized, it owns the raw pointer. This means that the smart pointer is responsible for deleting the memory that the raw pointer specifies. The smart pointer destructor contains the call to delete, and because the smart pointer is declared on the stack, its destructor is invoked when the smart pointer goes out of scope.

Access the encapsulated pointer by using the familiar pointer operators, -> and \*, which the smart pointer class overloads to return the encapsulated raw pointer.


The following example shows how a *unique_ptr* smart pointer type could be used to encapsulate a pointer to a large object.

```c
class LargeObject {
public:
    void DoSomething() {}
};

void ProcessLargeObject(const LargeObject& lo) {}

void SmartPointerDemo() {
    // Create the object and pass it to a smart pointer
    unique_ptr<LargeObject> pLarge(new LargeObject());

    // Call a method on the object
    pLarge->DoSomething();

    // Pass a reference to a method
    ProcessLargeObject(*pLarge);

} //pLarge is deleted automatically when function block goes out of scope. 
```

The example demonstrates the following essential steps for using smart pointers.
1. Declare the smart pointer as an automatic (local) variable.
2. In the type parameter, specify the pointed-to type of the encapsulated pointer.
3. Pass a raw pointer to a new-ed object in the smart pointer constructor.
4. Use the overloaded -> and \* operators to access the object.
5. Let the smart pointer delete the object.


<br />

## Kinds of Smart Pointers

The `unique_ptr` allows exactly one owner of the underlying pointer. Can be moved to a new owner, but not copied or shared.

The `shared_ptr` is the reference-counted smart pointer. Use when you want to assign one raw pointer to multiple owners. The raw pointer is not deleted until all `share_ptr` owners have gone out of scope or have otherwise given up ownership.

The `weak_ptr` is a special-case smart pointer for use in conjunction with `shared_ptr`. A `weak_ptr` provides access to an object that is owned by one or more `shared_ptr` instances, but does not participate in reference counting. Use when you want to observe an object, but do not require it to remain alive. Required in some cases to break circular references between `shared_ptr` instances.









