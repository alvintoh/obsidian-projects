Automatic Default Constructor
If we do not provide any custom constructors, the C++ compiler provides an automatic default constructor for our class for free!

The automatic default constructor will only initialize all member variables to their default values.

![[Custom Default constructor.png]]

![[Custom Constructors.png]]

![[Custom Constructors Example.png]]

Automatic Default Constructor
If any custom constructor is defined, automatic default constructor is not defined

![[Default Constructor error.png]]

In C++, a copy constructor is a special constructor that exists to make a copy of an existing object

![[Automatic Copy Constructor.png]]

![[Custom Copy Constructor example.png]]

![[Copy Constructor Example.png]]

Copy Constructor Invocation
Often, copy constructors are invoked automatcally:
* Passing an object as a parameter (by value)
* Returning an object from a function (by value)
* Initializing a new object

![[Default and Copy Constructor.png]]

![[Copy Constructors Example 2.png]]

![[Copy Constructor Example 3.png]]

![[Copy Constructor Example 4.png]]

In C++, a copy assignment operator defines the behavior when an object is copied using the assignment operator =.

![[Copy Constructor vs. Assignment.png]]

![[Automatic Assignment Operator.png]]

![[Custom Assignment Operator.png]]

![[Custom Assignment Example.png]]
![[Variable Storage Theory.png]]

![[Direct Storage.png]]

![[Storage by Pointer.png]]

![[Storage by Reference.png]]

![[Cube Currency Example.png]]

![[By Value example.png]]

![[By Reference example.png]]

![[By Pointer Example.png]]

![[By Value Exercise 2.png]]

![[By Ref Exercise 2.png]]

![[By Pointer Example 2.png]]

![[Return by Value theory.png]]

When an instance of a class is cleaned up, the class destructor is the last call in a class's lifecycle.

![[Automatic Default destructor.png]]

![[Custom Destructor.png]]

![[C++ Auto Destructor function called.png]]

Custom Destructor
A custom destructor is essential when an object allocates an external resource that much closed or freed when the object is destroyed. Examples:
* Heap memory
* Open files
* Shared memory

## Resetting deleted pointers to nullptr

Now that we've reviewed initialization, especially for pointers, let's talk about why you should manually reset pointers to nullptr when you're done with them.

Note that using "delete" on a pointer frees the heap memory allocated at that address. However, deleting the pointer does not change the pointer value itself to "nullptr" automatically; you should do that yourself after using "delete", as a safety precaution. For example:

```
// Allocate an integer on the heap:
int* x = new int;
// Now x holds some memory address to a valid integer.
// Do some kind of work with the integer.
// We'll just set that integer to 7:
*x = 7;
// Now delete the pointer to deallocate the heap memory:
delete x;
// This destroys the integer on the heap and frees the memory.
// But now x still holds the memory address!
// Set x to nullptr for safety:
x = nullptr;
```

The idea here is that by manually setting x to nullptr after "delete x", we help prevent two kinds of problems:

1. We don't want to delete the same allocated address more than once by mistake, which could cause errors. Using "delete" on nullptr does nothing, so this way, if we accidentally try to delete the same address twice, nothing further happens.

2. We must never dereference a pointer to deallocated memory. This could cause the program to crash with a segfault, exhibit strange behavior, or cause a security vulnerability. However, attempting to dereference a nullptr will almost always cause a segfault and terminate the program immediately. This is actually better than causing a silent security vulnerabilty or another problem that is harder to detect! Therefore, it makes sense to set the deleted pointer to nullptr, thus ensuring that if we dereference it carelessly, then it will cause a very obvious runtime error that we can fix.

You should also note that we only need to use delete and nullptr with pointers, of course. Variables in stack memory don't need to be manually deleted. Those are automatically deallocated when they go out of scope. (Please refer to the other reading lesson on scope.)

Assignment for Week 3
A class called Pair has already been declared, but the constructors have not been implemented yet. Pair has two public member variables:

int *pa,*pb;

These two "pointers to int" are intended to point to heap memory locations that store integers. The remainder of the Pair class expects the following functionality.

-   A single constructor Pair(int a, int b): This should set up pa and pb to point to newly allocated memory locations on the heap. The integers at those memory locations should be assigned values according to the constructor's integer arguments a and b.
    
-   A copy constructor Pair(const Pair& other): This takes as its argument a read-only reference to another Pair. It should set up the newly constructed Pair as a "deep copy," that is, it should create a new Pair that is equivalent to the other Pair based on dereferenced values but does not reuse any of the same memory locations. In other words, the copy constructor should set up its own instance's member variables pa and pb to point to newly allocated memory locations for integers on the heap; those memory locations must be new, not the same locations pointed to by the other Pair, but the integers at these new locations should be assigned values according to the integers that the other Pair is pointing to.
    
-   A destructor ~Pair() that de-allocates all of the the heap memory that had previously been allocated for this Pair's members.
    

The types of these member functions have already been declared in the declaration of Pair. Now you need to provide the implementation of each of these three member functions.

(Note: The function declarations shown in the code comment below do not include parameter names for the arguments. They show only the types of the arguments. This is allowed for a declaration, but when you define the implementation of those functions, you should give names to the parameters so that you can refer to them.)

```
/* Class Pair has already been declared
 * as shown in the following comments:
 *
  class Pair {
    public:
      int *pa,*pb;
      Pair(int, int);
      Pair(const Pair &);
      ~Pair();
* };
* Implement its member functions below.
*/
  Pair::Pair(int a, int b) {
    pa = new int, pb = new int;
    *pa = a;
    *pb = b;
  }

  Pair::Pair(const Pair & obj) {
    pa = new int, pb = new int;
    *pa = *(obj.pa);
    *pb = *(obj.pb);
  }

  Pair::~Pair() {
    delete pa;
    delete pb;
  }
 
 
 /* Here is a main() function you can use
  * to check your implementation of the
  * class Pair member functions.
  */
  
int main() {
  Pair p(15,16);
  Pair q(p);
  Pair *hp = new Pair(23,42);
  delete hp;
  
  std::cout << "If this message is printed,"
    << " at least the program hasn't crashed yet!\n"
    << "But you may want to print other diagnostic messages too." << std::endl;
  return 0;
}
```