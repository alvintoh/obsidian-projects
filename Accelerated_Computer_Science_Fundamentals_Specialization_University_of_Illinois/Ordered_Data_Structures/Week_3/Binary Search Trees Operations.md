# Balanced BST
Balanced BSTs are height-balanced trees that ensures nearly half of the data is located in each subtree
## BST Insert
* We identify the deepest node in the tree that is out of balance
BST Rotation
* To turn a stick into a mountain: break the stick in half, raise it up as a mountain, and reattach the children

## Generic Left rotation
Consider an arbitary tree such that
* The deepest point of imbalance is at node b
* The balance factor of b is 2
* The balance factor of c is 1.
* An insert in t3 ort4 caused the imbalanced

![[Generic Left Rotation.png]]

* Move b to be under c
## BST insert
We identify the deepest node in the tree that is out of balance:
* We "unbend" the elbow with a rotation about the bend and then we have a stick
![[BST Rotation.png]]

## Generic Right-Left Rotation
Consider an arbitrary tree such that:
* The deepest point of imbalance is at node b
* The balance factor of b is 2.
* The balance factor of c is -1
* An insert in t2 or t3 cause the imbalance

![[Generic Right Left rotation.png]]

![[Generic Right Left rotation in action.png]]

![[Rotation summary.png]]

## BST Rotations
* BST rotations restore the balance property to a tree after an insert causes a BST to be out of balance
* Four possible rotations: L, R, LR, RL
	* Rotations are local operations
	* Rotations do not impact the broader tree.
	* Rotations run in O(1) time.
* These trees are called "AVL Trees"

## AVL Trees
Balanced BSTs that are kept in balance through tree rotations on insert and remove are called AVL trees, named after Adelson-Velsky and Landis.
* To quickly compute the balance factor, AVL trees store the height of every node as part of the node itself

![[AVL Insert.png]]

![[AVL Remove.png]]

* An AVL Tree is an implementation of a balanced Binary Search Tree (BST)
* An implementation of an AVL tree starts with a BST implementation and adds two key ideas:
	- Maintains the height at each node
	- Maintains the balance factor after insert and remove

## B-tree Insertion
m -> refers to the length of the keys
For a B-tree "of order m"
* All keys within a node are in sorted order
* Each node contains no more than m-1 keys
* Each internal node can have at most m children so a B-tree of order m is like an m-way tree
*![[B-Tree Insertion.png]]

![[B-Tree Recursive Search.png]]

B-Tree Properties
For a B-tree "of order m":
1. All keys within a node are in sorted order.
2. Each node contains no more than m-1 keys
3. Each internal node has exactly one more child than key (at most m children, so a B-tree of order an m-way tree).
	- A root node can have a leaf or have [2, m] children
	- Each non-root, internal node has [ceil(m/2), m] children
4. All leaves are on the same level.

![[B-Tree in action and finding the order of m.png]]

![[B Tree Search Code.png]]

![[BTree Analysis.png]]

## Week 3 Challenge
```
/*
The height of a node is the number of edges in
its longest chain of descendants.

Implement computeHeight to compute the height
of the subtree rooted at the node n. Note that
this function does not return a value. You should
store the calculated height in that node's own
height member variable. Your function should also
do the same for EVERY node in the subtree rooted
at the current node. (This naturally lends itself
to a recursive solution!)

Assume that the following includes have already been
provided. You should not need any other includes
than these.

#include <cstdio>
#include <cstdlib>
#include <iostream>
#include <string>

You have also the following class Node already defined.
You cannot change this class definition, so it is
shown here in a comment for your reference only:

class Node {
public:
  int height; // to be set by computeHeight()
  Node *left, *right;
  Node() { height = -1; left = right = nullptr; }
  ~Node() {
    delete left;
    left = nullptr;
    delete right;
    right = nullptr;
  }
};
*/

void computeHeight(Node *n) {
  // Implement computeHeight() here.
  if( nullptr == n ) {
    return;
  } else{
    Node *leftNode = n->left;
    computeHeight( leftNode );
    Node *rightNode = n->right;
    computeHeight( rightNode );
    if( nullptr == leftNode && nullptr == rightNode ) {
      n->height = 0;
    } else if( nullptr == leftNode && nullptr != rightNode ) {
      n->height = 1 + rightNode->height;
    } else if( nullptr == rightNode && nullptr != leftNode ) {
      n->height = 1 + leftNode->height;
    } else {
      if ( leftNode->height >= rightNode->height ) {
        n->height = 1 + leftNode->height;
      } else {
        n->height = 1 + rightNode->height;
      }
    }
    return;
  }
}

// This function prints the tree in a nested linear format.
void printTree(const Node *n) {
  if (!n) return;
  std::cout << n->height << "(";
  printTree(n->left);
  std::cout << ")(";
  printTree(n->right);
  std::cout << ")";
}

// The printTreeVertical function gives you a verbose,
// vertical printout of the tree, where the leftmost nodes
// are displayed highest. This function has already been
// defined in some hidden code.
// It has this function prototype: void printTreeVertical(const Node* n);

// This main() function is for your personal testing with
// the Run button. When you're ready, click Submit to have
// your work tested and graded.
int main() {
  Node *n = new Node();
  n->left = new Node();
  n->right = new Node();
  n->right->left = new Node();
  n->right->right = new Node();
  n->right->right->right = new Node();

  computeHeight(n);

  printTree(n);
  std::cout << std::endl << std::endl;
  printTreeVertical(n);
  
  // The Node destructor will recursively
  // delete its children nodes.
  delete n;
  n = nullptr;

  return 0;
}
```