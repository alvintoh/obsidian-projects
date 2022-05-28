Arrays:
1. Elements are all the same type.
2. The size (number of bytes) of te type of data is known.

We can calculate the offset to any given index from the start of the array

![[Array offset and index.png]]

![[Array capacity and size.png]]

![[Std vector.png]]

![[Cube array capacity and size example.png]]

![[Linked list.png]]

![[List Node constructor.png]]

![[Linked List example.png]]

![[Linked List memory.png]]
![[Transverse linked list.png]]

![[Linked insert at front.png]]

![[Linked list add object example.png]]

![[Compare array with linked list.png]]

![[Sum of all required copies.png]]

![[Square time complexity.png]]

![[Linear complexity.png]]

![[Linear complexity calculation.png]]

![[Array resized time complexity.png]]

![[Run time analysis Big O notation.png]]

![[big o of data in sorted array.png]]

![[big o of find data in array and list.png]]

![[big of insert after.png]]

![[big o of delete after.png]]

![[double linked list with next and previous linked field.png]]

![[big o of queue.png]]

![[queue theory.png]]

![[big o of stack.png]]
![[Stack theory.png]]

  
Lab Assignment
```
#include <iostream>
#include <stack>
#include <queue>

std::stack<int> reverse_stack(std::stack<int> s) {
  std::stack<int> reversed_s;
  
  // write code here that returns a stack whose elements are
  // in reverse order from those in stack s
  while (!s.empty()){
    reversed_s.push(s.top());
    s.pop();
  }

  return reversed_s;
}

std::queue<int> reverse_queue(std::queue<int> q) {
  std::queue<int> reversed_q;
  std::stack<int> s;
  
  // write code here that returns a queue whose elements are
  // in reverse order from those in queue q
  while (!q.empty()){
    s.push(q.front());
    q.pop();
  }
  while (!s.empty()){
    reversed_q.push(s.top());
    s.pop();
  }

  return reversed_q;
}

void print_stack(std::string name, std::stack<int> s) {
  std::cout << "stack " << name << ": ";
  while (!s.empty()) {
    std::cout << s.top() << " ";
    s.pop();
  }
  std::cout << std::endl;
}

void print_queue(std::string name, std::queue<int> q) {
  std::cout << "queue " << name << ": ";
  while (!q.empty()) {
    std::cout << q.front() << " ";
    q.pop();
  }
  std::cout << std::endl;
}

int main() {
  std::stack<int> s, rs;
  std::queue<int> q, rq;
  
  s.push(1); s.push(2); s.push(3); s.push(4); s.push(5);

  print_stack("s",s);

  rs = reverse_stack(s);

  print_stack("reversed s",rs);
  
  q.push(1); q.push(2); q.push(3); q.push(4); q.push(5);
  
  print_queue("q",q);
  
  rq = reverse_queue(q);
  
  print_queue("reversed q",rq);

  return 0;
}
```
```
