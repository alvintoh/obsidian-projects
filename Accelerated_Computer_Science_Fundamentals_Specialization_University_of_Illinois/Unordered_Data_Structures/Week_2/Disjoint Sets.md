The representative member of the set is the first number of the set e.g 2, 7, 0, 3

![[Disjoint Sets.png]]

![[Disjoint Sets Introset.png]]

As you read further literature in computer science, you'll notice that the "disjoint sets" data structure is also sometimes referred to as the "union-find" data structure, because of its primary methods, "union" and "find".

However, there is another important thing to watch out for: In C and C++, the word "union" is reserved for a specific language feature, so you can't use "union" as a name for a variable or function. Instead you have to use a variant such as "set_union" and so on.

![[Disjoint Set Naive Implementation.png]]

![[Better Implementation of Disjoint Sets.png]]

![[UpTrees.png]]

![[Disjoint Sets implementing UpTrees.png]]

![[Disjoint Sets Find.png]]

![[Disjoint Sets Smart Union.png]]

![[Disjoint Sets Smart Union by Height and Size.png]]

![[Path Compression.png]]

![[Disjoint Sets Analysis.png]]

![[Big O of Disjoint Sets.png]]

### Challenge
Modify the implementation of DisjointSets::find(int i) below so that it uses path compression during queries.

The DisjointSets class here models a collection of one or more disjoint sets of items. This is very similar to the professor's description of "up trees"; imagine that each set is a tree, where the root of the tree represents the set it belongs to, while other items in the same set refer to it (directly or indirectly).

Given a DisjointSets instance "d", the array d.s contains one integer for each item in the entire collection. Currently, this array is statically allocated with 256 integers, so the entire collection can involve at most 256 items. For any given item with index i, the value recorded at d.s[i] represents either the parent of item i, or a more distant ancestor of item i, or the root of the entire set that item i belongs to. If the value of d.s[i] is -1, then this means that item i is the root of its own set.

The provided code for find does this much already:

1.  The find function queries for the ultimate root of a given item, with index i.
    
2.  If the array entry for index i is less than 0, then return i, as it is the root of its own set. (This is the base case.)
    
3.  Otherwise, the array entry currently records an ancestor of node i in the tree, but not the root. So, recurse on the ancestor index. Assume that find() succeeds in recursion: it returns the root of this set. (This assumption would be the inductive hypothesis if you were writing a proof of correctness by induction.)
    
4.  Return the root that was found. (This fulfills the assumption that was made when we recursed in the previous step.)
    

You need to add the path compression feature to this find function. This means you must record the information that was found recursively as an update to the array before the function returns. This optimizes subsequent calls to the function.

In summary, after calling find(i) on one of the elements in the set, i, the find function should return the root index of the disjoint set (the index of its root element) and also update the "s" array to ensure that element i and every ancestor of i will refer directly to the root.

```
#include <iostream>
#include <vector>

class DisjointSets {
public:
	int s[256];

	DisjointSets() { for (int i = 0; i < 256; i++) s[i] = -1; }

	int find(int i);
};

/* Modify the find() method below to
 * implement path compression so that
 * element i and all of its ancestors
 * in the up-tree refer directly to the
 * root after that initial call to find()
 * returns.
 */

int DisjointSets::find(int i) {
 static std::vector<int> path;
 if(s[i] < 0) {
   for(auto iter = path.begin(); iter != path.end(); iter++) {
     int node = *iter;
     s[node] = i;
   }
   return i;
 } else{
   path.push_back(i);
   return find(s[i]);
 }
}

int main() {
  DisjointSets d;

  d.s[1] = 3;
  d.s[3] = 5;
  d.s[5] = 7;
  d.s[7] = -1;

  std::cout << "d.find(3) = " << d.find(3) << std::endl;
  std::cout << "d.s(1) = " << d.s[1] << std::endl;
  std::cout << "d.s(3) = " << d.s[3] << std::endl;
  std::cout << "d.s(5) = " << d.s[5] << std::endl;
  std::cout << "d.s(7) = " << d.s[7] << std::endl;

  return 0;
}
```