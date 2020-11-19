---
layout: post
title:  "Unique_Ptr in C++"
categories: [ C++ Concepts ]
tags: [ C++, Smart Pointers, RAII, Unique_Ptr ]
similar: [ C++ Pointers]
featured: false
hidden: false
---

<br />

This article and the examples are from the [Microsoft C++ Documentation](https://docs.microsoft.com/en-us/cpp/cpp/how-to-create-and-use-unique-ptr-instances?view=msvc-160){:target="_blank"}. 

A `unique_ptr` does not share its pointer. It cannot be copied to another `unique_ptr`, passed by value to a function, or used in any C++ Standard Library algorithm that requires copies to be made. A `unique_ptr` can only be moved. This means that the ownership of the memory resource is transferred to another `unique_ptr` and the original `unique_ptr` no longer owns it.



<br />

## Examples

#### Example 1

The following example shows how to create `unique_ptr` instances and pass them between functions. These are usually the 3 ways to create `unique_ptr` instances. It shows that the `unique_ptr` can be moved, but not copied. "Moving" transfers ownership to a new `unique_ptr` and resets the old `unique_ptr`.

```c
unique_ptr<Song> SongFactory(const std::wstring& artist, const std::wstring& title) {
    // Implicit move operation into the variable that stores the result.
    return make_unique<Song>(artist, title);
}

void MakeSong() {
    // Create a new unique_ptr with a new object.
    auto song = make_unique<Song>(L"Mr. Children", L"Namonaki Uta");

    // Use the unique_ptr.
    vector<wstring> titles = { song->title };

    // Move raw pointer from one unique_ptr to another.
    unique_ptr<Song> song2 = std::move(song);

    // Obtain unique_ptr from function that returns by value.
    auto song3 = SongFactory(L"Michael Jackson", L"Beat It");
}
```

#### Example 2

The following example shows how to create `unique_ptr` instances and use them in a vector.
```c
void SongVector() {
    vector<unique_ptr<Song>> songs;

    // Create a few new unique_ptr<Song> instances
    // and add them to vector using implicit move semantics.
    songs.push_back(make_unique<Song>(L"B'z", L"Juice"));
    songs.push_back(make_unique<Song>(L"Namie Amuro", L"Funky Town"));
    songs.push_back(make_unique<Song>(L"Kome Kome Club", L"Kimi ga Iru Dake de"));
    songs.push_back(make_unique<Song>(L"Ayumi Hamasaki", L"Poker Face"));

    // Pass by const reference when possible to avoid copying.
    for (const auto& song : songs) {
        wcout << L"Artist: " << song->artist << L"    Title: " << song->title << endl;
    }
}
```

In the range for loop, notice that the `unique_ptr` is passed by reference. If you try to pass by value here, the compiler will throw an error because the `unique_ptr` copy constructor is deleted.


#### Example 3

The following example shows how to initialize a `unique_ptr` that is a class member.
```c
class MyClass {
private:
    // MyClass owns the unique_ptr.
    unique_ptr<ClassFactory> factory;

public:
    // Initialize by using make_unique with ClassFactory default constructor.
    MyClass() : factory (make_unique<ClassFactory>()) {

    }

    void MakeClass() {
        factory->DoSomething();
    }
}
```

#### Example 4

You can use `make_unique` to create a `unique_ptr` to an array, but you cannot use `make_unique` to initialize the array elements.

```c
// Create a unique_ptr to an array of 5 integers.
auto p = make_unique<int[]>(5);

// Initialize the array.
for (int i = 0; i < 5; i ++) {
    p[i] = i;
    wcout << p[i] << endl;
}
```





