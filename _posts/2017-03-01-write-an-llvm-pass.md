---
layout: post
title:  "Write an LLVM Pass"
categories: [ Tutorial ]
tags: [ LLVM ]
similar: [ LLVM ]
featured: true
hidden: true
---

<br />

In this post, I will show how I write an LLVM pass. I will also share how I solve some common problems which are not addressed in LLVM documents and tutorials. Note that this post is about how to write a new pass, not a Hello pass in most LLVM tutorials.

<br />

### Part 0: Install LLVM

```
mkdir llvm-source
```

Version matters in LLVM. Make sure you download the same version of LLVM and Clang, and also read the tutorials and documents for that particular version. Do not download directly from the svn repository unless you are LLVM developers. If you are just using LLVM, download the stable releases will save you lots of effort. Download the LLVM and Clang from [`this link`](http://releases.llvm.org/download.html).

To install LLVM and Clang (I use 3.4.2 as an example, other versions should be similar):

```
tar xvzf llvm-3.4.2.src.tar.gz
mv llvm-3.4.2.src src
tar xvzf cfe-3.4.2.src.tar.gz
mv cfe-3.4.2.src src/tools/clang
```

Then install LLVM:

```
cd llvm-source
mkdir build
cd build
./../src/configure
make
```

Done!

<br />

### Part 1: Write a New Pass

First, I will show you how to write a Candy pass.

```
cd llvm-source/build/lib/Transforms
mkdir Candy
vim Candy.cpp
```

Copy the following lines into Candy.cpp:

```c
#include "llvm/Pass.h"
#include "llvm/IR/Function.h"
#include "llvm/Support/raw_ostream.h"

using namespace llvm;

namespace {
    struct Candy : public FunctionPass {
        static char ID;
        Candy() : FunctionPass(ID) {}

        virtual bool runOnFunction(Function &F) {
            errs() << "Candy: ";
            errs().write_escaped(F.getName()) << '\n';
            return false;
        }
    };
}

char Candy::ID = 0;
static RegisterPass<Candy> X("candy", "Candy Pass", false, false);
```

Then copy the following lines into Makefile:

```c
# Makefile for candy pass

# Path to top level of LLVM hierarchy
LEVEL = ../../..

# Name of the library to build
LIBRARYNAME = Candy

# Make the shared library become a loadable module so the tools can
# dlopen/dlsym on the resulting library.
LOADABLE_MODULE = 1

# Include the makefile implementation stuff
include $(LEVEL)/Makefile.common
```

If you write a new pass (instead of Hello), for example Candy, by following the tutorials above, you will probably run into the following error:

```
make: *** No rule to make target ‘/path/to/llvm-source/src/lib/Transforms/Candy/Makefile’, needed by ‘Makefile’. Stop.
```

This is because you write your new path in the **build/** directory, and LLVM cannot find it in the src/ directory. Here is what you need to do to solve it.

```
cd llvm-source/src/lib/Transforms
mkdir Candy
cd Candy
vim Candy.cpp (save and exit, you don’t need to write anything in the file)
vim Makefile (copy the above Makefile into this one)
cd ..
vim CMakeLists.txt
```

Add the following line into llvm-source/src/lib/Transforms/CMakeLists.txt:

```
add_subdirectory(Candy)
```

Add one more file llvm-source/src/lib/Transforms/Candy/CMakeLists.txt with following lines:

```c
add_llvm_loadable_module(LLVMCandy
    Candy.cpp
)
```

Then build LLVM again:

```
cd llvm-source/build
./../src/configure
make -j8
```

Then go to Candy and make again, the error message will disappear.

Write a program that you would like to run the candy analysis, and compile it into bitcode file:

```
cd llvm-source
mkdir projects
cd projects
vim test.cpp (write a program that you would like to run the analysis)
clang -O0 -emit-llvm -c test.cpp -o test.bc
```

Then run the following command to analyze it:

```
../../build/Release+Asserts/bin/opt -load 
../../build/Release+Asserts/bin/Candy.so -candy < test.bc > /dev/null
```


<br />

### Part 2: Write a Pass with Multiple Files

In this part, I will show you how to include a Sweet.cpp and Sweet.h into your Candy pass.

```
cd llvm-source/build/lib/Transforms/Candy
mkdir include
mkdir src
cd include
vim Sweet.h (write your Sweet.h and save it)
cd ../src
mkdir Sweet
cd Sweet
vim Sweet.cpp (write your Sweet.cpp and save it)
vim Makefile
```

Copy the following into your /llvm-source/build/lib/Transforms/Candy/src/Sweet/Makefile

```c
# Path to top level of LLVM hierarchy
LEVEL = ../../../../..

# Name of the library to build
LIBRARYNAME = Sweet

BUILD_ARCHIVE = 1

# Include the makefile implementation stuff
include $(LEVEL)/Makefile.common
```

Copy the following into your /llvm-source/build/lib/Transforms/Candy/src/Makefile

```c
# Path to top level of LLVM hierarchy
LEVEL = ../../../..

DIRS = Sweet

# Include the makefile implementation stuff
include $(LEVEL)/Makefile.common
```

Modify your /llvm-source/build/lib/Transforms/Candy/Makefile

```c
# Makefile for candy pass

# Path to top level of LLVM hierarchy
LEVEL = ../../..

# Name of the library to build
LIBRARYNAME = Candy

# Make the shared library become a loadable module so the tools can
# dlopen/dlsym on the resulting library.
LOADABLE_MODULE = 1
DIRS = src
EXTRA_DIST = include
# Include the makefile implementation stuff
include $(LEVEL)/Makefile.common
```

Add the corresponding files to your /llvm-source/src/lib/Transforms/Candy

```
cd llvm-source/src/lib/Transforms/Candy
mkdir include
mkdir src
cd include
vim Sweet.h (an empty file is okay)
cd ../src
mkdir Sweet
cd Sweet
vim Sweet.cpp (an empty file is okay)
```

Add the three Makefile above to the corresponding directory. Also modify the /llvm-source/src/lib/Transforms/Candy/CMakeLists.txt

```c
add_llvm_loadable_module(LLVMCandy
    Candy.cpp
    src/Sweet/Sweet.cpp
)
```

Build LLVM again:

```
cd llvm-source/build
./../src/configure
make -j8
```

Then go to your Candy pass, you will be able to make your Candy pass with Sweet.cpp.

```
cd llvm-source/build/lib/Transforms/Candy
make
```

However, when you try to run your pass with your test files, you will probably run into the following error:

```
../../build/Release+Asserts/bin/opt: symbol lookup error: ../../build/Release+Asserts/lib/Candy.so: undefined symbol: _Z21runSweetRN4llvm8FunctionE
```

To solve this problem, you need to modify your /llvm-source/build/lib/Transforms/Candy/Makefile. Add the following line into your Makefile:

```
USEDLIBS = Sweet.a
```

Try to make and run the analysis again. You will not see the error!
