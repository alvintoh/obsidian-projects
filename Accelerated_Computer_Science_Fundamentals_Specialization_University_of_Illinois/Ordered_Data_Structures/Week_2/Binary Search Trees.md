#  Terminology
* Each element in our tree is a node:
* Each connection between two nodes is an edge :->
* Trees must always contain a root node that has no incoming edges
* Nodes that contain no outgoing edges are called leaf nodes
* Edges do not have name, but are referred to by the nodes they connect: K -> M
* Parent Node = 1
* Node children = anywhere from 0 to infinite children
* Sibling -> same level
* Nodes share a common ancestor
* Grandchild / grandchildren childnode that exists 2 layers under a parent node
* Grandparent parentnode that exist 2 layers up a grandchild node
* Ancestor nodes are node that are directly the parent of the given node, and it can exist laters up a current node
* 3 conditions for tree
	1.  Must have a root
	2. Must have directed edges (direction of arrow moves down from root node)
	3. Must not have a cycle (a loop exists from current node edge to  any existing node)
We say a tree is a "rooted, directed, and acyclic (does not have a cycle)" structure

# Binary Tree
* A binary tree is a tree where every node has at most two children
* 
## Binary Tree Properties
* Every child is labeled as either the "left child" or "right child" of its parent
* The height of a binary tree is the number of edges in the longest path from the root to a leaf
* A binary tree is full if and only if every node has either zero children or two children
* A binary tree is perfect if and only if all interior nodes have two children and leaves at the same level
* A perfect binary tree of height h has `2^(h + 1) – 1` node.
* A binary tree is complete if and only if the tree is complete up until the last level and all leaf nodes on the last level are pushed to the left

Puzzle:
Is a full tree complete? No
Is a complete tree full? No

# Tree Traversals
* PreOrder Traversal
* InOrder Traversal
* PostOrder Traversal
* LevelOrder Traversal (Search layer by layer of treenode)

Traversal -> requires every node to be visit
Search -> may not visit every single node, may use strategy to find, and search ends when the node is found

# Binary Search Tree
  A binary tree is a BST if for every node in the tree:
	* Nodes in the left subtree are less than itself
	* Nodes in the right subtree are greater than itself

## BST-Based Dictionary
A BST used to implement a dictionary will store both a key and data at every node

## BST Remove
* Zero children: Simple, delete the node
* One child: Simple, works like a linked list
* Find the IOP of the node to be removed
* Swap with the IOP
* Remove the node in its new position

## BST
Binary Search Trees (BSTs) can take on many forms and structures, even containing the same data
* This can be affected by the insert order
* e.g Insert Order 4, 2, 3, 6, 7, 1, 5 vs 1, 3, 2, 4, 5, 7, 6
* The number of possible way to insert the data into a BST is 7 ! () =n ! (nth factorial)
* 
![[Comparison of Data Structure Big O.png]]

* The Height Balance factor (b) of a node is the difference in height between its two subtrees
* Height balance factor = Height(Right Subtree) - Height(Left Subtree) 
* if Empty tree = -1 (Use that as a value to compute)

### Balanced BST
* A balanced BST is a BST where every node's balance factor has a magnitude of 0 or 1
![[Balanced BST with workings.png]]
* The worst-case BST will have a height proportional to the number of nodes
* An average BST will have a heigh proportional to the logarithm of the number of nodes
* Using a height balance factor, we can formalize if a given BST is balanced
* There are n nodes. Excluding the root node, every node must have a pointer pointing to it, i.e., n-1 not-null pointers.

So, no. Of null pointers = 2n - (n - 1) = n+1

Graded Quiz

```
/********************************************************
You may assume that the following Node class has already
been defined for you previously:

class Node {
public:
  Node *left, *right;
  Node() { left = right = nullptr; }
  ~Node() {
    delete left;
    left = nullptr;
    delete right;
    right = nullptr;
  }
};

You may also assume that iostream has already been included.

Implement the function "int count(Node *n)" below to return
an integer representing the number of nodes in the subtree
of Node n (including Node n itself).

*********************************************************/

int count(Node *n) {
  if (n == NULL)
    return 0;
  else {
    return 1 + count(n-> left) + count(n-> right);
  }
}

int main() {
  Node *n = new Node();
  n->left = new Node();
  n->right = new Node();
  n->right->left = new Node();
  n->right->right = new Node();
  n->right->right->right = new Node();

  // This should print a count of six nodes
  std::cout << count(n) << std::endl;

  // Deleting n is sufficient to delete the entire tree
  // because this will trigger the recursively-defined
  // destructor of the Node class.
  delete n;
  n = nullptr;

  return 0;
}
```