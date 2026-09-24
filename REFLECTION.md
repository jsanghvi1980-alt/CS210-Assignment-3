# Assignment 3 Reflection


### 1. Why does LinkedList::deleteFront() need two delete calls?

It needs two delete calls because two different things were created with new. The object
stored in data was created in main.cpp with new data, so delete -> data frees that object.
The node was created inside addFront() with new Node<T>, so delete frees the node from itself.

### 2. Why did changing ArrayList from values to pointers make a destructor necessary?

When the array stored regular values, C++ automatically destroyed those values when the ArrayList disappeared.
After changing it to an array of pointers, the actual objects were created on the heap with new, so the ArrayList
became responsible for deleting them. Forgetting the destructor would cause a memory leak, but the compiler would 
not report an error because the code is still legal in C++. 

### 3. How do addFront() and search() treat pointer ownership differently?

addFront() takes ownership of the pointer it receives, which means the list becomes responsible for deleting that object
later. search() only borrows the pointer long enough to compare its value with the objects in the list. It must never delete
the search pointer because it does not own it.

### 4. What two mechanisms allowed you to switch between LinkedList and ArrayList without changing main.cpp?

The first mechanism was polymorphism through the List<T> interface and its virtual functions. Both ArrayList and LinkedList inherit 
from List<T>, so main.cpp can use either one through the same type of pointer. The second mechanism was the makeList() factory function,
which lets us choose the implementation in one place.

### 5. Choose one important keyword from this assignment and explain why it matters.

The keyword I chose is virtual, especially for the destructor in List<T>. The program stores the real ArrayList or LinkedList inside a List<T>
pointer so the virtual destructor makes sure the correct derived destructor runs when the list is deleted. Without it, the stored objects and linked list
nodes might not be cleaned up, causing a memory leak.