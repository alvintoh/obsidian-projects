A heap is a complete binary tree T is a min-heap if:
* T = {} or
* T = {r, TL, TR}, where r is less than the roots of {TL ,TR} and {TL, TR} are min-heaps.
* T = 4
![[Min Heap calculation.png]]

![[Min Heap Insert.png]]

![[Heap insert code.png]]

![[Remove min node from Heap.png]]

![[Remove Heap code.png]]

![[Three ways to build heap.png]]

![[Heapifydown operations down in linear o n.png]]

![[HeapSort explanation.png]]

HeapSort is useful
* Does not use any additional space in the array in memory
* Very convenient to do this sort entirely in memory. 
* A heap sort is going to be an ideal sort that allows us to order the data and provide some benefits for being in-memory, 
* Give us some advantages if the data structure is already semi-sorted.

Question: When using an array to store a complete tree, why is the root node stored at index 1 instead of at the front of the array at index 0?
Answer: This makes the math for finding children and parents simpler to compute and to explain.

Question: How many nodes of a complete binary tree are leaf nodes?
Answer: About half.

Question:  Recall that the heapifyDown procedure takes a node index whose children (if any) are heaps, but the value of the node might not satisfy the heap property compared to its children's values. This procedure then swaps the node's value with the smallest child value larger than it (if any), and then calls itself on that smallest child node it just swapped values with to further propagate that value down the heap until it finds a valid location for it.

```
template <class T>
void Heap<T>::_heapifyDown(int index) {
    if (!_isLeaf(index)) {
        T minChildIndex = _minChild(index);
        if (item_[index] > item_[minChildIndex] ) {
            std::swap( imem_[index], item_[minChildI]);
            _heapifyDown(minChildIndex);
        }
    }
}
```

When you call heapifyDown on a given node, what is the maximum number of times heapifyDown is called (including that first call) to find a valid location for the initial value of that node?
Answer: The maximum number of times heapifyDown is called is one plus the height of the node.

Assignment
Implement downHeap(Node *n) for a min heap data structure, that is here implemented as a node-based binary tree with an integer member variable "value" and left and right child pointers. (Unlike the video lesson which implemented downHeap on an array implementation of a complete binary tree, the binary tree in this challenge problem is not stored as an array and is not necessarily complete; any node might have only a left child, only a right child, both, or neither.)

The starter code below defines a class called "Node" that has two child pointers ("left" , "right") and an integer "value" member variable. There is also a constructor Node(int val) that initializes the children to nullptr and the node's value to val.

Your job is to implement the procedure "downHeap(Node *n)" . The procedure should assume that n->left is the root of a min heap subtree (or nullptr) and the same for n->right. The value at Node *n (specifically n->value) might not be less than the values in its left subtree and in its right subtree, and so the tree with Node *n as its root might not be a min heap (even though its left subtree and right subtree are both min heaps). Your code should modify the tree rooted at Node *n so it is a min heap. You do not need to balance the tree or turn it into a complete tree. You only need to ensure that the tree satisfies the min heap property:

For a min heap, it is okay for a node's value to be _equal_ to one or both of its children, but the node's value must not be _greater_ than either of its children. You should not perform swaps with nodes of equal value, as this does needless work.

Again, as is implied by the above description, for this exercise you may assume that **only** the root node violates the min heap property at the beginning, if any node does (as the left and right subtrees are already valid heaps). This means it's possible to implement the downHeap function as O(\log n)O(logn). If your algorithm has a running time worse than O(\log n)O(logn), it is probably incorrect. The significance of this O(\log n)O(logn) algorithm is that it can be used as an efficient tool in the O(n)O(n)-time algorithm that corrects a new heap in multiple steps from the bottom up, as described in lecture.

```
/*

Below, please implement the downHeap procedure for
a min heap data structure, which we will represent
as node-based tree for this exercise (not an array).

Suppose you are given a tree where the left and right
subtrees are min heaps, but the root node in particular
might not maintain the min heap property. Your code
should modify the tree rooted at Node* n so it is a
min heap. This means you need to satisfy the min heap
property: it is okay for a node's value to be equal to
one or both of its children, but the node's value must
not be greater than either of its children.

Tips:
Unlike the video lessons which demonstrated downHeap
implemented with an array implementation, this assignment
uses an ordinary binary tree with left and right child
pointers. This ordinary binary tree might not be complete
or balanced: any node might have only one child or the
other, or both, or neither. (You do not have to try to
balance the tree or turn it into a complete tree.)

If the root node exists, and if it has a left or right
child, and if one of the children has a smaller value
than the root node, then you should swap the root node
with the smaller child to move the large value down
into the tree. (This may need to be done recursively.)
Be careful to check whether pointers are null before
dereferencing them, as always; that includes using "->"
to access a class member through a pointer. In addition,
you must be careful not to accidentally compare "left"
and "right" pointers directly if you really intend to
compare the stored values "left->value" and "right->value".

Assume that these headers have already been included
for you:

#include <iostream>
#include <string>

You have the following class Node already defined.
You cannot change this class definition, so it is
shown here in a comment for your reference only:

class Node {
public:
  int value;
  Node *left, *right;
  Node(int val = 0) { value = val; left = right = nullptr; }
  ~Node() {
    delete left;
    left = nullptr;
    delete right;
    right = nullptr;
  }
};

This function has also previously been defined for you:

void printTreeVertical(const Node* n);

You can use it to print a verbose, vertical diagram of
a tree rooted at n. In this vertical format, a left child
is shown above a right child in the same column. If no
child exists, [null] is displayed.

*/

Node* children_node(Node *n) {
  if( nullptr != n->left && nullptr != n->right ) {
      if(n->left->value <= n->right->value) {
        return n->left;
      } else {
        return n->right;
      }
  } else if( nullptr == n->left && nullptr != n->right) {
    return n->right;
  } else if( nullptr == n->right && nullptr != n->left ) {
    return n->left;
  } else {
    return nullptr;
  }
}

void downHeap(Node *n) {
  // Implement downHeap() here.
  Node *child_node = children_node(n);
  if(nullptr != child_node) {
      if(child_node->value < n->value) {
        auto temp = child_node->value;
        child_node->value = n->value;
        n->value = temp;
        downHeap(child_node);
      } else {
        return;
      }
  }
  return;
}

// You can also use this compact printing function for debugging.
void printTree(Node *n) {
  if (!n) return;
  std::cout << n->value << "(";
  printTree(n->left);
  std::cout << ")(";
  printTree(n->right);
  std::cout << ")";
}

int main() {
  Node *n = new Node(100);
  n->left = new Node(1);
  n->right = new Node(2);
  n->right->left = new Node(3);
  n->right->right = new Node(4);
  n->right->right->right = new Node(5);

  downHeap(n);

  std::cout << "Compact printout:" << std::endl;
  printTree(n);
  std::cout << std::endl << "Vertical printout:" << std::endl;
  printTreeVertical(n);

  delete n;
  n = nullptr;

  return 0;
}

```