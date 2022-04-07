![[C++ Variable introduction.png]]

Every C++ variable has four things:
* A name
* A type
* A value
* A location in memory ("memory address")

A Variable's Memory Address
In C++, the & operator returns the memory address of a variable. 

![[C++ Memory address.png]]

Stack Memory
By default, every variable in C++ is placed in stack memory.

Stack memory is associated with the current function and the memory's lifecycle is tied to hte function:
* When the function returns or ends, the stack memory of that function is released.

![[Stack Memory.png]]

![[C++ Memory address stack.png]]

![[Memory address stack declining.png]]
![[Pasted image 20220320232953.png]]

![[Deference Operator.png]]

![[C++ Stack memory trace.png]]

![[C++ Memory example.png]]

Heap memory allows us to create memory independent of the lifecycle of a function

![[C++ New Operator.png]]

![[Heap Memory.png]]

![[C++ Stack and Heap.png]]

![[C++ Heap memory.png]]

![[NullPointer in C++.png]]

![[Arrow Operator.png]]

![[Stack Heap Memory more examples.png]]

![[Tracing the stack memory of pointers.png]]

![[Tracing the Stack and Heap Memory.png]]

![[Deference example 3.png]]

![[Array in C++.png]]

**.h** files are "header files". These usually have definitions of objects and declarations of global functions. Recently, some people name header files with a ".hpp" suffix instead.

**.cpp** files are often called the "implementation files," or simply the "source files". This is where most function definitions and main program logic go.

In general, the header files contain _declarations_ (where classes and custom types are listed by name and type, and function prototypes give functions a type signature) while the source files contain _implementation_ (where function bodies are actually defined, and some constant values are initialized). It becomes easier to understand this organizational separation if you know more about how the code is compiled into a program you can run. Let's look at the **cpp-class** example from the provided code.

Note the **#pragma once** at the beginning. Instructions beginning with **#** are special commands for the compiler, called preprocessor directives. This instruction prevents the header file from being automatically included multiple times in a complex project, which would cause errors.

This header file also includes the declaration of the Cube class, including listing its members, but the definition doesn't give the full source code of the functions here. For example, the body of the setLength function is not written here! Only the signature of the function is given, to declare its input argument types and return type. Instead, the function will be defined in the Cube.cpp source code file.

Notice that the first thing it does is **#include "Cube.h"** to include all the text from the Cube.h file in the same directory. Because the filename is specified in quotes, as "Cube.h", the compiler expects it to be in the same directory as the current file, Cube.cpp. Below we'll see a different way to refer to filenames using **< >** instead.

Then, the file gives the definitions for the functions from the class definition before. These full source code listings for the functions that were declared previously are called the implementation. (It is common that function bodies will be implemented in the cpp file and _not_ in the h file, but sometimes _short_ class function bodies will be defined directly in the h file where they are declared inside the class declaration. The compiler handles that situation in a special way automatically so that it doesn't cause problems in the linking stage, which is described below.)

This time there are two #include directives! First, it includes a standard library header from the system directory. This is shown by the use of **< >**. When you write **#include <iostream>**, the compiler will look for the **iostream** header file in a system-wide library path that is located outside of your current directory.

Next, it does **#include "Cube.h"** just like in the Cube.cpp file. You have to include the necessary headers in every cpp file where they are needed. However, you shouldn't use #include to literally include one cpp file in another! **There is no need to write #include "Cube.cpp"** because the function definitions in the Cube.cpp file will be compiled separately and then _linked_ to the code from the main.cpp file. You don't need to know all the details of how this works, but let's look at a diagram that shows the general idea:

![[Pasted image 20220322175003.png]]

The Cube.cpp files and main.cpp files make requests to include various header files. (The compiler might automatically skip some requests because of **#pragma once** to avoid including multiple times in the same file.) The contents of the requested header files will be temporarily copied into the cpp source code file where they are included. Then, the cpp file with all of its extra included content will be compiled into something called an **object file**. (Our provided examples keep the object files hidden in a subdirectory, so you don't need to bother with them. But, if you see a file that has a **.o** extension, that is an object file.) Each cpp file is separately compiled into an object file. So, in this case Cube.cpp will be compiled into Cube.o, and main.cpp will be compiled into main.o.

Although each cpp file needs the appropriate headers included for compilation, that has to do with checking type information and declarations. The compiled object files are allowed to rely on _definitions_ that appear in the other object files. That's why it's okay that main.cpp doesn't have the Cube function definitions included: as long as main.cpp does know about the type information from the Cube function signatures in Cube.h, the main.o file will be "**linked against"** the compiled definitions in the Cube.o file. (I don't know why we say "link against" instead of "link with" when we talk about this, but that is the usual terminology!) The linker program will also link against system-wide object files, such as for **iostream**. After the compiler and linker programs finish processing your code, you will get an executable file as a result. In this case, that file is simply named **main**.

Fortunately, you won't have to configure the compiler manually in this course. We will provide a **Makefile** to you for each project, which is a kind of script that tells the compiler how to build your program. We'll talk more about that in the next reading lesson.

```
#include <iostream>

// This class Pair has already been defined for you.
// (You may not change this definition.)
class Pair {
public:
  int first, second;
  void check() {
    first = 5;
    std::cout << "Congratulations! The check() method of the Pair class \n has executed. (But, this isn't enough to guarantee \n that your code is correct.)" << std::endl;
  }
};

// Insert your declaration and implementation of the function pairFactory()
// below, by replacing "..." with proper C++ code. Be sure to declare the
// function type to return a pointer to a Pair.
Pair *pairFactory() {
  // ...
  // (You can use as many lines as you want.)
  Pair *p = new Pair;
  return p;
}

// Your function should be able to satisfy the tests below. You should try
// some other things to convince yourself. If you have a bug in this problem,
// the usual symptom is that after you submit, the grader will crash with a
// system error. :-)
int main() {
  Pair *p;
  p = pairFactory();
  
  // This function call should work without crashing:
  p->check();
  
  // Deallocating the heap memory. (Assuming it was made on the heap!)
  delete p;

  std::cout << "If you can see this text, the system hasn't crashed yet!" << std::endl;  

  return 0;
}

```