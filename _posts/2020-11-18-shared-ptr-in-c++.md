---
layout: post
title:  "Shared_Ptr in C++"
categories: [ C++ Concepts ]
tags: [ C++, Smart Pointers, RAII, Shared_Ptr ]
similar: [ C++ Pointers ]
featured: false
hidden: false
---

<br />

This article and the examples are from the [Microsoft C++ Documentation](https://docs.microsoft.com/en-us/cpp/cpp/how-to-create-and-use-shared-ptr-instances?view=msvc-160){:target="_blank"}. 


The `shared_ptr` type is a smart pointer that is designed for scenarios in which more than one owner might have to manage the lifetime of the object in memory. After you initialize a `shared_ptr` you can copy it, pass it by value in function arguments, and assign it to other `shared_ptr` instances. 

All the instances point to the same object, and share access to one "control block" that increments and decrements the reference count whenever a new `shared_ptr` is added, goes out of scope, or is reset. When the reference count reaches zero, the control block deletes the memory resource and itself.


<br />

## Examples

#### Example 1

This example shows how to include the required headers and declare the required types to use the `shared_ptr`. It also shows how to create a `shared_ptr`.

```c
#include <algorithm>
#include <iostream>
#include <memory>
#include <string>
#include <vector>

using namespace std;

struct MediaAsset {
    virtual ~MediaAsset() = 0; // make it polymorphic
};

struct Song : public MediaAsset {
    wstring artist;
    wstring title;
    Song(const wstring& artist_, const wstring& title_) :
        artist{ artist_ }, title{ title_ } {}
};

struct Photo : public MediaAsset {
    wstring date;
    wstring location;
    wstring subject;
    Photo(const wstring& date_, const wstring& location_, const wstring& subject_) : 
        date{ date_ }, location{ location_ }, subject{ subject_ } {}
};

int main() {
    // Use make_shared function when possible.
    auto sp1 = make_shared<Song>(L"The Beatles", L"Im Happy Just to Dance With You");

    // Another way to create a shared_ptr, but less efficient.
    shared_ptr<Song> sp2(new Song(L"Lady Gaga", L"Just Dance"));

    // When initialization must be separate from declaration, 
    // initialize with nullptr to make your programming intent explicit.
    shared_ptr<Song> sp5(nullptr);
    sp5 = make_shared<Song>(L"Elton John", L"Im Still Standing");
}
```

Whenever possible, use the make_shared function to create a `shared_ptr` when the memory resource is created for the first time. It is exception-safe. It uses the same call to allocate the memory for the control block and the resource, which reduces the construction overhead. 


#### Example 2

The following example shows how to declare and initialize `shared_ptr` instances that take on shared ownership of an object that has already been allocated by another  `shared_ptr`. Assume that sp2 is an initialized `shared_ptr` as in Example 1.
```c
// Initialize with copy constructor. Increments ref count.
auto sp3(sp2);

// Initialize via assignment. Increments ref count.
auto sp4 = sp2;

// Initialize with nullptr. sp7 is empty.
shared_ptr<Song> sp7(nullptr);

// Initialize with another shared_ptr. sp1 and sp2 swap pointers as well as ref counts.
sp1.swap(sp2);
```








