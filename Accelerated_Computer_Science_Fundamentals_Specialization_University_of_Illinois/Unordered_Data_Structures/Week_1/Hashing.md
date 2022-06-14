# Goals
We want to define a keyspace, a (mathematical) description of the keys for a set of data

... use a function to map the keyspace into a small set of integers

A Hash Table consist of three things:
1. Hash Function
2. An Array
3. Collision Handling

![[A Perfect Hash Function.png]]

![[A bad Hash function for dice probablity.png]]

## Hash Function
Our hash function consists of two parts:
* A hash: Transform input -> int value
* A compression: % N

Choosing a good hash function is tricky...
* Don't create your own (yet*)
* Very smart people have created very bad hash functions

Characteristics of a good function
* Computation Time: O(1) Running Time
* Deterministric:
* Satisfy the SUHA: 
	* h(a) h(b)  
	* p(h(a) == h(b)) = 1/N if a != b

![[General Purpose Hash function.png]]

* Ensure every keyspace is uniquely spaced to avoid hash collision

![[Collision Handling and load factor.png]]
Alpha is the load factor
* A load factor of 1.0 means that you have exactly as much data in the table as there is space in the array. 

* A load factor of 0.5 means on average, the arrays have four or we have linked lists that wouldn't fill up half the array or half the table if we put them in there. 

* A load factor of two means on an average, every single node has two items in the linked list. So, you can see as a load factor grows, the amount of time it takes to run this algorithm is also going to grow

![[Probe Based Hashing.png]]

![[Linear probing to explain probe based Hashing.png]]

![[Double Hashing.png]]

![[Running Times of these methods.png]]

![[Linear Probing vs Double Hashing running times.png]]

Double Hashing to maintain good alpha ratio:
* Have to resize the array often
![[Rehashing the array.png]]

If we consider this example right here, we might have originally hashed something to index 1. When we expand the array, that hash of index 1 may have been at one or it may have been at index 8 or 9, depending on the size of the array. Because of this, we need to make sure that when we expand the size of the array, we go through and rehash every single value in the array to make sure it's in the proper spot.

![[Summary of hash.png]]

A hash table is a fantastic general purpose data structure, while an AVL is going to solve particularly great problems. If all you care is a lookup, the hash table is the algorithm for you.

![[Red Black Trees (AVL, BST) in C++.png]]

![[Hash table in C++.png]]

### Challenge
Suppose we have a simple hash table that consists of a vector of integers. We can preallocate the table to have a specific size and fill the values with -1 to begin with, to mark those elements empty. For simplicity, this table will actually be a _hash set_ rather than a _hash map_; in other words, rather than mapping unique keys to values, we simply have a collection of unique keys, so it is not a dictionary ADT. Such a table merely answers the question of whether any given integer is part of the set (can be found) or is not part of the set (cannot be found).

In the code below, you need to implement the insert function:

`1  2  int insert(int value, std::vector<int> &table);` 

This insert function should first compute a specific hash function of _value_. This hash function should return the least-significant three decimal digits (a number from 0 to 999) of the variable _value_. This hash result should be used as an index into the thousand-element vector _table_ that has been previously initialized with -1 in each element. If the element at this location of _table_ is available (currently set to -1), you can replace the element with _value_. If this location is not available (currently set to some other value than -1) then you should check the next element, repeatedly, until you find an available element and can store _value_ there. The insert() function should then return the number of times a location in the hash table was identified to store the given _value_ but was not available.

Example: If your function is able to insert the value in the hash location on the first try, return 0. If your function has to check the next two locations before finding an empty space, return 2.

The main() procedure below will create an appropriate table, then create 500 random values and call insert() on each one of them to insert them into the table. At the end, this procedure will report the length of the longest cluster encountered when inserting a value (as reported by your insert() function) and then print out the contents of the hash table so you can see how clusters form. Since the original hashed position will be the three least significant digits of the value stored there, it will be easy to see which values had to be relocated by linear probing, and how much probing was needed.

When you submit your code, the length of the longest cluster encountered when inserting a value as reported by your insert() function will be compared to the result from the reference code for correctness.

```
#include <iostream>
#include <iomanip>
#include <vector>
#include <algorithm>
#include <functional>

int insert(int value, std::vector<int> &table) {
  // Code to insert value into a hashed location in table
  // where table is a vector of length 1000.
  // Returns the number of collisions encountered when
  // trying to insert value into table.
  int hashKey = value % 1000;
  int collisions = 0;
  
  if(table[hashKey] == -1) {
    table[hashKey] = value;
  } else {
    while(table[hashKey] != -1) {
      collisions++;
      hashKey++;
    }
    table[hashKey] = value;
  }
  return collisions;
}

int main() {
  // Prepare some random but distinct values
  constexpr int NUM_VALUES = 500;
  std::vector<int> value(NUM_VALUES);
  int prev_value = 0;
  for (int i = 0; i < NUM_VALUES; i++) {
    prev_value += rand()%25 + 1;
    value[i] = prev_value;
  }

  // Create hash table of size 1000 initialized with -1
  std::vector<int> table(1000,-1);

  // Insert values and track the maximum number of collisions
  int max_hit = 0, max_value = -1;
  for (int i = 0; i < NUM_VALUES; i++) {
    int hit = insert(value[i],table);
    if (hit > max_hit) {
      max_hit = hit;  
      max_value = value[i];
    }
  }

  std::cout << "Inserting value " << max_value << " experienced " << max_hit << " collisions." << std::endl <<std::endl;

  // Print the table contents
  for (int j = 0; j < 1000; j += 10) {
    std::cout << std::setw(3) << j << ":";
    for (int i = 0; i < 10; i++) {
      if (table[j+i] == -1)
        std::cout << "      ";
      else
        std::cout << std::setw(6) << table[j+i];
    }
    std::cout << std::endl;
  }

  return 0;
}

```