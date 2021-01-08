---
layout: post
title:  "Online Book Reader System Problem"
categories: [ Object-Oriented Design ]
tags: [ C++, OOD ]
similar: [ OOD ]
featured: false
hidden: false
sidenav: OODProblems
excerpt: Design the data structures for an online book reader system which provides the following functionality.
---

<br />

## Description

Design the data structures for an online book reader system which provides the following functionality:
1. User membership creation and extension.
2. Searching the database of books.
3. Reading a book.
4. Only one active user at a time.
5. Only one active book by this user.


<br />

## C++ Implementation

Below is a complete C++ implementation of the online book reader problem.

To implement the above operations, we need User, Book, UserManager, and Library classes. We also use a OnlineReaderSystem class. We use this class to store information about all books, deals with user managerment. 


```c
#include <iostream>
#include <map>

using namespace std;

class Book {
private:
    static int bookId;
    int thisBookId;
    string bookDetail;
public:
    Book(string detail) {
        thisBookId = bookId;
        bookId ++;
        setBookDetail(detail);
    }
    int getBookId() {
        return thisBookId;
    }

    string getBookDetail() {
        return bookDetail;
    }
    void setBookDetail(string detail) {
        bookDetail = detail;
    }
};

class User {
private:
    static int userId;
    int thisUserId;
    string userName;
    int accountType;
public:
    User(string name, int type) {
        thisUserId = userId;
        userId ++;
        setUserName(name);
        setAccountType(type);
    }
    int getUserId() {
        return thisUserId;
    }
    string getUserName() {
        return userName;
    }
    void setUserName(string name) {
        userName = name;
    }
    int getAccountType() {
        return accountType;
    }
    void setAccountType(int type) {
        accountType = type;
    }
    // Extend membership. Not implemented yet.
    void renewMembership() {}
};

class Library {
private:
    map<int, Book*> books;
public:
    void addBook(Book* book) {
        int id = book->getBookId();
        if (books.find(id) != books.end()) 
            return;
        books[id] = book;
        return;
    }
    void removeBookById(int id) {
        if (books.find(id) != books.end())
            books.erase(id);
    }
    void removeBook(Book* book) {
        int id = book->getBookId();
        removeBookById(id);
    }
    Book* findBook(int id) {
        if (books.find(id) == books.end()) 
            return nullptr;
        else
            return books[id];
    }
};

class UserManager {
private:
    map<int, User*> users;
public:
    void addUser(User* user) {
        int id = user->getUserId();
        if (users.find(id) != users.end())
            return;
        users[id] = user;
        return;
    }
    void removeUserById(int id) {
        if (users.find(id) != users.end())
            users.erase(id);
    }
    void removeUser(User* user) {
        int id = user->getUserId();
        removeUserById(id);
    }
    User* findUser(int id) {
        if (users.find(id) == users.end())
            return nullptr;
        else
            return users[id];
    }
};

class OnlineReaderSystem {
private:
    Library* library;
    UserManager* userManager;
    Book* activeBook;
    User* activeUser;
public:
    OnlineReaderSystem() {
        library = new Library();
        userManager = new UserManager();
    }
    Library* getLibrary() {
        return library;
    }
    UserManager* getUserManager() {
        return userManager;
    }
    Book* getActiveBook() {
        return activeBook;
    }
    void setActiveBook(Book* book) {
        activeBook = book;
    }
    User* getActiveUser() {
        return activeUser;
    }
    void setActiveUser(User* user) {
        activeUser = user;
    }
};

int Book::bookId = 0;
int User::userId = 0;

int main() {
    OnlineReaderSystem ors;
    Book* book1 = new Book("Design Pattern");
    Book* book2 = new Book("OOD");
    User* user1 = new User("Alice", 1);
    User* user2 = new User("Bob", 1);

    ors.getLibrary()->addBook(book1);
    ors.getLibrary()->addBook(book2);
    ors.getUserManager()->addUser(user1);
    ors.getUserManager()->addUser(user2);

    ors.setActiveUser(user1);
    ors.setActiveBook(book2);
}
```

The decision to tear off user management and library into their own classes, when this functionality could have been in the general OnlineReaderSystem class, is an interesting one. On a very small system, making this decision could make the system overly complex. However, as the system grows, and more and more functionality gets added to OnlineReaderSystem, breaking off such components prevents this main class from getting overwhelmingly lengthy.