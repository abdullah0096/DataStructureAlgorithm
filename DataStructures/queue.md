# Queue Data Structure in C++

## 1. Introduction to Queue
A **Queue** is a linear data structure that follows the **FIFO (First In, First Out)** principle. This means that elements are added at one end (rear) and removed from the other end (front).

### Characteristics of a Queue:
- **FIFO Order**: The first element inserted is the first to be removed.
- **Two Main Operations**:
  - **Enqueue**: Adds an element to the rear.
  - **Dequeue**: Removes an element from the front.

## 2. Queue Operations
A queue supports the following operations:
- **Enqueue(x)**: Inserts `x` at the rear.
- **Dequeue()**: Removes the front element.
- **Front() / Peek()**: Retrieves the front element without removing it.
- **IsEmpty()**: Checks if the queue is empty.

## 3. Time Complexity of Queue Operations
- **Enqueue, Dequeue, Peek:** `O(1)` as they involve adding or removing an element from either end.

## 4. Queue Implementation
### 4.1 Using an Array
```cpp
#include <iostream>
#define SIZE 5

class Queue {
    int arr[SIZE];
    int front, rear;
public:
    Queue() { front = -1; rear = -1; }
    bool isFull() { return rear == SIZE - 1; }
    bool isEmpty() { return front == -1 || front > rear; }
    void enqueue(int x) {
        if (isFull()) { std::cout << "Queue Overflow"; return; }
        if (front == -1) front = 0;
        arr[++rear] = x;
    }
    void dequeue() {
        if (isEmpty()) { std::cout << "Queue Underflow"; return; }
        front++;
    }
    int peek() { return isEmpty() ? -1 : arr[front]; }
};
```

### 4.2 Using a Linked List
```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

class Queue {
    Node *front, *rear;
public:
    Queue() { front = rear = nullptr; }
    bool isEmpty() { return front == nullptr; }
    void enqueue(int x) {
        Node* temp = new Node(x);
        if (rear == nullptr) front = rear = temp;
        else { rear->next = temp; rear = temp; }
    }
    void dequeue() {
        if (isEmpty()) return;
        Node* temp = front;
        front = front->next;
        if (!front) rear = nullptr;
        delete temp;
    }
    int peek() { return isEmpty() ? -1 : front->data; }
};
```

### 4.3 Using Circular Queue
Circular queues improve space utilization by reusing freed spaces.

### 4.4 Using Two Stacks
A queue can be implemented using two stacks, one for enqueue and one for dequeue operations.

## 5. Applications of Queue
- **Task Scheduling**: CPU scheduling, I/O buffering.
- **Graph Algorithms**: Breadth-First Search (BFS).
- **Request Handling**: Web servers, print queues.
- **Real-world Queues**: Ticket counters, call centers.

## 6. Queue Implementation in C++
### Using C++ STL `std::queue`
```cpp
#include <iostream>
#include <queue>

int main() {
    std::queue<int> q;
    q.push(10);
    q.push(20);
    std::cout << "Front: " << q.front() << "\n";
    q.pop();
    std::cout << "Front after pop: " << q.front() << "\n";
    return 0;
}
```

## 7. STL `std::queue` in C++
### Common Functions
- `push(x)`: Adds `x` to the queue.
- `pop()`: Removes the front element.
- `front()`: Returns the front element.
- `back()`: Returns the last element.
- `empty()`: Checks if the queue is empty.

## 8. Variants of Queue
- **Circular Queue**: Overcomes the issue of wasted space in a linear queue.
- **Priority Queue**: Elements are dequeued based on priority.
- **Deque (Double-Ended Queue)**: Allows insertion and deletion from both ends.

## 9. Comparison of Queue with Other Data Structures
### Queue vs Stack
- **Queue**: FIFO order.
- **Stack**: LIFO order (Last In, First Out).

### Queue vs Deque
- **Queue**: Insert at rear, delete from front.
- **Deque**: Insert and delete from both ends.

## 10. Example Problems and Solutions Using Queues
### Implementing a Queue Using Two Stacks
```cpp
#include <iostream>
#include <stack>

class QueueUsingStacks {
    std::stack<int> s1, s2;
public:
    void enqueue(int x) { s1.push(x); }
    void dequeue() {
        if (s2.empty()) {
            while (!s1.empty()) { s2.push(s1.top()); s1.pop(); }
        }
        if (!s2.empty()) s2.pop();
    }
    int front() {
        if (s2.empty()) {
            while (!s1.empty()) { s2.push(s1.top()); s1.pop(); }
        }
        return s2.empty() ? -1 : s2.top();
    }
};
```

### Reversing a Queue Using a Stack
```cpp
#include <iostream>
#include <queue>
#include <stack>

void reverseQueue(std::queue<int> &q) {
    std::stack<int> s;
    while (!q.empty()) {
        s.push(q.front());
        q.pop();
    }
    while (!s.empty()) {
        q.push(s.top());
        s.pop();
    }
}
```

### Generating Binary Numbers Using a Queue
```cpp
#include <iostream>
#include <queue>

void generateBinaryNumbers(int n) {
    std::queue<std::string> q;
    q.push("1");
    for (int i = 0; i < n; i++) {
        std::string s = q.front(); q.pop();
        std::cout << s << " ";
        q.push(s + "0");
        q.push(s + "1");
    }
}
```

## 11. Conclusion
Queues are fundamental data structures used in various applications, from scheduling tasks to handling network requests. Understanding their implementations, STL usage, and variations like circular and priority queues enhances problem-solving skills.

