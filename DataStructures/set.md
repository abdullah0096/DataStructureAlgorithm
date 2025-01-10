# Set

- A set is a data structure that stores <b>UNIQUE</b> elements, i.e. no duplicates.
    - A set may be sorted (ordered-set) or unsorted (unordered-set)
    - If set is sorted then it is implemented using self-balancing binary search tree (e.g. Red-Black Tree)
    - If set is unsorted, then implemented using Hash-Tables

## Operations
- Insert : Add an element to the set if it does not exist
- Delete : Remove an element from the set if it exists
- Search : Check membership of an element

## Time complexity
- Ordered set  - O(log n) for insertion, deletion, and search.
- Unordered set - O(1) average and O(n) worst-case for all operations.

## Application
- To remove duplicate from a dataset
- Performing mathematical operation like union, intersection, difference
- To check if an element belong to a set (i.e. membership) efficiently

---

# Set in C++
STL provides ```std::set``` as associative container (key-value, key) that stores unique elements in a sorted order. Elements are sorted in ascending order (or using a custom comparator).

## Types of containers
- <b>Ordered associative container</b>
    - Elements are ```ALWAYS``` sorted, implemented using tree-based structure (red-black tree).
    - ```std::set``` : Unique elements (also known as keys)
    - ```std::multiset``` : DUPLICATE allowed
    - ```std::map``` : Stores Key-value pair with unique keys, sorted by keys 
    - ```std::multimap``` : Allows duplicate keys with key-value pairs, sorted by keys.

- <b>Unordered Associative Containers</b>
    - Elements ```NOT``` sorted but provide fast average case operations (I, D, S). Implemented using Hash-Table
    - ```std::unordered_set``` : Unique keys, unordered
    - ```std::unordered_multiset``` : Duplicate keys, unordered
    - ```std::unordered_map``` : Key-value pairs with unique keys, unordered
    - ```std::unordered_multimap``` : Key-value pairs with duplicate keys, unordered.

> HashTable in C++-STL is implemented as ```std::map``` and ```std::unordered_map```

- <b>Sequence Container</b>
    - Store elements in a linear sequence.
    - ```set::vector``` - Dynamic array with random access
    - ```set::list``` (Doubly L.L.), ```std::deque``` (Queue)

- <b>Container Adapters</b>
    - ```std::stack``` : LIFO (Last In, First Out) interface.
    - ```std::queue``` : FIFO (First In, First Out) interface.
    - ```std::priority_queue``` : Sorted elements with a priority interface.

## Functions of Containers : (TODO)



## In built functions on ```std::set```
- ```insert()```: Adds an `element if it does not already exist.
- ```erase()```: Removes an element by value or iterator.
- ```find()```: Searches for an element.
- ```count()```: Checks if a value exists (returns 0 or 1).
- ```clear()```: Removes all elements.
- ```size()```: Returns the number of elements.
- `begin()`, `end()`, `rbegin()`, `rend()`

```cpp
#include <iostream>
#include <set>

int main() {
    // Create a set and insert elements
    std::set<int> s;
    s.insert(5);
    s.insert(2);
    s.insert(8);
    s.insert(3);

    // Print the set elements
    std::cout << "Set elements: ";
    for (int x : s) {
        std::cout << x << " ";
    }
    std::cout << "\n";

    // Find an element
    int toFind = 3;
    auto it = s.find(toFind);
    if (it != s.end()) {
        std::cout << "Element " << toFind << " found in the set.\n";
    } else {
        std::cout << "Element " << toFind << " not found in the set.\n";
    }

    // Count occurrences of an element
    int toCount = 5;
    if (s.count(toCount)) {
        std::cout << "Element " << toCount << " exists in the set.\n";
    } else {
        std::cout << "Element " << toCount << " does not exist in the set.\n";
    }

    // Erase an element
    s.erase(8);
    std::cout << "Set after erasing 8: ";
    for (int x : s) {
        std::cout << x << " ";
    }
    std::cout << "\n";

    // Check the size of the set
    std::cout << "Size of the set: " << s.size() << "\n";

    // Clear the set
    s.clear();
    std::cout << "Set cleared. Is empty? " << (s.empty() ? "Yes" : "No") << "\n";

    return 0;
}

```

## Custom comparator
- Used for sorting in descending order
- Sorting based on custom criteria, such as by modulus, length of strings, etc.
- Custom comparators do not affect the performance of std::set operations. The complexity of operations remains O(log n).
- You can use lambdas for concise comparators or functors/functions for reusable and more complex logic.



```cpp

// Using functor
struct CustomCompare {
    bool operator()(int a, int b) const {
        return a > b; // Descending order
    }
};

// Using function
bool customCompare(int a, int b) {
    return a < b; // Ascending order (default behavior)
}

int main(){
    std::set<int, CustomCompare> s = {1, 3, 2, 5, 4};
    // ...

    // using Lambda
    auto compare = [](int a, int b) { return a % 10 < b % 10; }; // Sort by last digit
    std::set<int, decltype(compare)> s(compare);
    // ...

    // using functions
    std::set<int, decltype(&customCompare)> s(customCompare);   
}

```


`decltype` is a keyword used to determine the type of an expression at compile-time. 
It inspects the type of an expression without evaluating it. 
It is useful in `generic programming`, where the types may not be explicitly known.

> Syntax : `decltype(expression)`

---
`auto` VS `decltype`

`auto`: Deduces the type of a variable or function return value based on the initializer or expression it is assigned.

`decltype`: Deduces the type of an expression without evaluating it. 
It reveals the exact type of the expression as it exists.

---

## Self-balancing Binary Search Tree (BST)

A self-balancing binary search tree is a type of binary search tree that keeps its height as small as possible after every insertion or deletion. 
This ensures efficient operations like search, insert, and delete, which have a time complexity of `O(log n)`, where `n` is the number of elements in the tree.

- BST
    - For each node in a BST : 
        - All elements in the `left` subtree are smaller than the parent.
        - All elements in the `right` subtree are larger than the parent.
    - It is roughly balanced structure - the height difference between the left and right subtrees of any node is kept minimal.
    - Height of Balanced-BST : O(log n)
    - Height of Unbalanced BST : O(n) in the worst case
    - After every insertion or deletion, rotations (may) be performed to ensure balance
    - Types of BST :
        - `Red-Black`
        - `AVL` : Height difference at most 1
        - `Splay`, `B-Trees`, `B+ Trees`

```cpp
Without Balancing (Unbalanced Tree):
If you insert elements in sorted order (e.g., 1, 2, 3, 4, 5), the tree becomes as follows.

1
 \
  2
   \
    3
     \
      4
       \
        5

Search for 5 takes O(n).
```
```cpp
With Balancing

      3
    /    \
   2      5
  /      / 
 1     4   

Search for 5 takes O(logn).
```